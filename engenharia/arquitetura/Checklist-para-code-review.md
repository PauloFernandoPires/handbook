Seguem os pontos que precisam ser analisados em qualquer merge request pelo revisor de forma a atestar uma qualidade mínima no código que será aceito para a master.

Vale lembrar que, todos os pontos de verificação já devem ser analisados pelo desenvolvedor da funcionalidade para acelerar esse processo.

De forma geral, o revisor **não deve** realizar as correções no código. Os problemas devem ser apontados para que o desenvolvedor realize as correções.

# Itens obrigatórios para verificação pelo revisor

- A existência de warnings do Stylecop
- A existência de messages do Code Analysis
  - O Code Analysis precisa ser executado em toda a solução pois o padrão do Visual Studio, por padrão, só vai mostrar mensagens dos arquivos abertos.
  - Para rodar o Code Analysis, entre em:
    - Analyze -> Run Code Analysis -> On Solution
- Se todos os testes unitários estão funcionando.
- Se todo os projetos da solução estão compilando. (CTRL+SHIFT+B)
- Se objetos que implementam IDisposable estão sendo descartados corretamente. Exemplos de classes que precisam disso:
  - DbContext
  - PdfDocument (do Spire.Doc)
  - HttpClient
- Se foi incluído código morto, precisa ser removido. Exemplos:
  - Código comentado.
  - Código após um return.
  - Variáveis não utilizadas.
- Se a nomenclatura de classes segue o padrão do projeto
  - Ainda não temos um padrão global em nossos projetos. Logo, o novo desenvolvimento deve seguir o padrão estabelecido naquele projeto. Mas, seguem alguns exemplos que precisam ser verificados.
    - Erros de português.
    - Se os nomes de pastas e namespaces estão no plural ou singular.
    - Se é utilizado '_' (underscore) ou não para nomes de classes, métodos, etc... ou simplesmente camelCase.
- Se o uso de switch está prevendo o caso de opção que não foi mapeada (default) levantando exceção. Ex:
```cs
switch (opcao){
  case 1 :
    return "ABERTO";
  case 2 :
    return "FECHADO";
  default:
    throw new InvalidOperationException("Opcao não mapeada: " + opcao);
}
```
- Caso o projeto tenha unit tests, eles precisam ser executados pelo revisor.

# Sobre o teste da funcionalidade em si
- O nível de teste no Merge Request depende do bom senso do revisor, conversa com a equipe e da complexidade da nova funcionalidade.
  - Exemplos:
    - Nova tela de formulário para o cadastro de uma informação: É preciso executar a aplicação e testar situações limites como:
      - Campos em branco
      - Campos com muita informação
      - Execução em 2 abas diferentes (caso a concorrência seja um problema)
    - Correção de bug pequeno: Somente a leitura do código no Code Review pode ser satisfatória.
    - Grande mudança de código: Se está planejado um teste integrado para essa grande mudança, o teste pode se resumir nesse primeiro momento a um teste de [caminho feliz](https://en.wikipedia.org/wiki/Happy_path).
- Durante os testes, é interessante acompanhar as queries de SQL que foram no banco para identificar algum problema do tipo [(N+1)](https://www.brentozar.com/archive/2018/07/common-entity-framework-problems-n-1/)

# Procedimentos adicionais
- Caso o revisor não tenha a permissão de maintainer para levar o branch para o master, ele deve usar a funcionalidade de **Aprovar** do Gitlab para deixar marcado sua opinião sobre o Merge Request. Essa funcionalidade é só um indicativo de opinião e não impacta em nada o código no repositório.
