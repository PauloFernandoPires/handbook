### FluentValidation
- O FluentValidation deve ser usado somente para validações simples de entrada de dados e que não dependam, por exemplo, de acesso a banco de dados para serem determinadas. Ou seja, a intenção do Fluent é só remover e facilitar o código escrito para validação de campos de formulário.
- O autor do projeto [não recomenda a validação automática](https://docs.fluentvalidation.net/en/latest/aspnet.html). Porém, é preciso avaliar cada caso. No caso de novos projetos MVC, parece ser uma boa solução pois:
  - É menos código escrito.
  - A responsabilidade da validação será pequena já que validações mais complexas serão realizadas na feature.

### Value Object
- Os objetos de domínio devem transformar propriedades representadas por primitivos (int, string, decimal) em Values Objects. 
- Só devem ser transformados em Value Objects, campos que tenham pelo menos dois [invariants](#invariant)
  - Exemplo, campo email: Email tem pelo menos 2 regras. Tem que ser uma string de x caracteres e precisa ter um '@' na string. Cabe ser transformado em um Value Object.
  - Exemplo, campo de descrição de alguma coisa: Normalmente só tem 1 tipo de regra (menor que 100 caracteres).
- Desse jeito, as regras associadas a essa informação ficam associadas diretamente ao Value Object e isso centraliza a regra de negócio para sua formação.
- Existem exemplos no curso [FluentValidation Fundamentals](#cursos-que-merecem-ser-vistos) que mostram como acoplar a validação de um campo com a criação de um Value Object. Assim, os dados de um formulário de entrada já podem ser validados contra a criação do Value Object. (Exemplo: o campo email já pode validar se está correto com o Value Object Email.)

Fontes: 
- [Functional C#: Primitive obsession](https://enterprisecraftsmanship.com/posts/functional-c-primitive-obsession/)
- [Collections and Primitive Obsession](https://vkhorikov.medium.com/collections-and-primitive-obsession-67c8bd6efe95)

### Always Valid Domain
- O objeto de domínio nunca pode ser carregado de qq forma. Ele sempre tem que representar um objeto que seja íntegro em relação ao sistema. Isso quer dizer que não podemos ter um objeto **Ato** abaixo sendo criado da seguinte forma:

```cs
var ato = new Ato()
{
    NaturezaID = (short)NaturezasEnum.MinutaAcordao,
    EmentaTexto = new Texto() { Descricao = "Ementa de exemplo" },
    AcordaoNumero = 13,
    AcordaoAno = 2022
};
```
- Essa forma de criação deixa muito aberta a possibilidade de criar um Ato que não esteja íntegro. 

- A forma sugerida de criação de entidades é via factory (método estático dentro da classe com nome **Create**) e definindo as propriedades do objeto somente com leitura (public set e private set).
```cs
public class EscolhaDeResponsavel : ValueObject
{
    private EscolhaDeResponsavel(bool responsavelPessoa, bool responsavelOrgao)
    {
        ResponsavelPessoa = responsavelPessoa;
        ResponsavelOrgao = responsavelOrgao;
    }

    public bool ResponsavelPessoa { get; }

    public bool ResponsavelOrgao { get; }

    public static Result<EscolhaDeResponsavel, Erro> Create(bool responsavelPessoa, bool responsavelOrgao)
    {
        if (!responsavelPessoa && !responsavelOrgao)
        {
            return Erros.Comandos.PrecisaSelecionarPeloMenosUmResponsavel();
        }

        return new EscolhaDeResponsavel(responsavelPessoa, responsavelOrgao);
    }
}
```
- A vantagem de criar o método estático é deixar preparado para criar qualquer regra de negócio que não permita a criação do objeto. Mesmo que não tenha nenhuma regra em um primeiro momento, é recomendável criar desse jeito para mantermos um padrão.
- Qualquer mudança de estado do objeto deve ser realizada via método. Assim, qualquer mudança passa por um filtro de validação antes de efetivar a mudança.

### Retorno de Validações
- Validações de FluentValidation devem retornar ValidationResult e serem tratadas diretamente na interface. Ou seja, O FluentValidation pode deixar de fazer parte da camada App de nossos sistemas e passa a ser um 'facilitador' de validação mais avançado que o Data Annotation.
- Os objetos de domínio que têm métodos para executar funcionalidades (Ex: Incluir opinião, Cadastrar dispositivo) podem ter métodos acessórios que realizem as validações necessárias no padrão Pode*. Exemplos:
```cs
  public Result<Opiniao, Erro> PodeIncluirOpiniao()
  public UnitResult<Erro> PodeCadastrarDispositivo()
```
- Esses métodos devolverão um objeto **Result<T, Erro>** ou **UnitResult<Erro>** que contém o erro de validação que não permite que a funcionalidade seja executada.
- Essa separação permite que o padrão CQRS fique da seguinte forma:
  - O QueryHandler pode chamar só o Pode*.
  - O CommandHandler pode chamar direto o método de execução que encapsula o Pode*.

### DDD Trilemma
- O DDD Trilemma diz que você pode não as três propriedades de DDD ao mesmo tempo. São elas:
  - Pureza: Nenhuma dependência a processos externos. 
  - Encapsulamento: Todas as regras de negócio estão dentro da camada de negócio.
  - Performance: Nenhuma chamada desnecessária a processos externos.

> Exemplo: Na criação de um email, é preciso validar se o nome do email não é igual a outro já cadastrado.
- A solução que perde em performance é passar a lista de todos os emails:
```cs
public static Result<Email, Error> Create(string input, Email[] allEmails)
{
    if (allEmails.Any(c => c.Value == input))
        return Errors.General.EmailIsTaken();

    return new Email(input);
}
```
- A solução que perde Pureza é passar o repositório para dentro do domínio.
```cs
public static Result<Email, Error> Create(string input, IEmailRepository emailRepository)
{
    if (emailRepository.EmailIsTaken(input))
        return Errors.General.EmailIsTaken();
 
    return new Email(input);
}
```
- A solução que perde Encapsulamento é realizar a validação do repositório em um método fora do Create (na Feature ou na Controller). Ou seja, a regra de negócio passou a ficar fora do domínio.
```cs
public static Result<Email, Error> Create(string input)
{
    return new Email(input);
}
```
- **Tente adotar a solução que perde performance quando possível.**
- **Caso, essa solução não possa ser adotada, a sugestão é seguir para solução de perder encapsulamento.** Ou seja, fazer a regra de validação fora da criação do objeto do domínio.
  - A explicação é que a regra de negócio é a parte mais importante da aplicação e passar a injetar dependências externas a ela mistura responsabilidades.
- Resumindo, essa é uma concessão que precisa ser realizada: **Prefira pureza do seu domínio sobre encapsulamento.**


### Cursos que merecem ser vistos
- [FluentValidation Fundamentals](https://app.pluralsight.com/library/courses/fluentvalidation-fundamentals/table-of-contents)
- [Refactoring from Anemic Domain Model Towards a Rich One](https://app.pluralsight.com/library/courses/refactoring-anemic-domain-model/table-of-contents)
- [CQRS in Practice](https://app.pluralsight.com/library/courses/cqrs-in-practice/table-of-contents)
- [Applying Functional Principles in C# 6](https://app.pluralsight.com/library/courses/csharp-applying-functional-principles/table-of-contents)

### Glossário
- #### Invariant 
  - [Invariants are generally business rules/enforcements/requirements that you impose to maintain the integrity of an object at any given time.](https://nikeshshetty.medium.com/designing-the-ddd-way-introduction-9acd910e418)