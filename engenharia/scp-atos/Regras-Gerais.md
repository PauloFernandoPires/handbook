## Naturezas de um Ato

| NaturezaID | Natureza                           |
|------------|------------------------------------|
| 1          | Minuta de Acórdão                  |
| 2          | Decisão Monocrática                |
| 3          | Despacho Monocrático               |
| 4          | Decisão Monocrática da Presidência |

### Minuta de Acórdão
- Usado para cadastrar atos que serão usados em sessões plenárias. Dentro do sistema, é chamado também de Relatório/Voto pois é o voto do Relator do Processo.

### Decisão Monocrática
- É uma decisão em si feita diretamente pelo Relator do processo que não precisa passar por uma sessão para ser válida.

### Despacho Monocrático
- É uma ação do Relator que não tem natureza decisória

### Decisão Monocrática da Presidência
- É uma decisão emitida pelo Presidente em exercício do Tribunal que tem efeito imediato. 
- É utilizada normalmente em períodos de recesso do Tribunal.
- Quando as sessões voltam a ocorrer, essas decisões passam pelo Plenário para serem referendadas.

## Relator Atual do Ato

- Ou é o Relator ou o Novo Relator. Nesse caso, o Conselheiro Substituto do Relator não cabe nessa validação. 
- Essa regra é usada, por exemplo, para saber se um usuário pode visualizar um ato enquanto está em elaboração. Um ato que tem um Conselheiro Substituto convocado, não deve permitir que o gabinete do Conselheiro Substituto o visualize. Somente o gabinete do Conselheiro "Original" pode visualizar. Essa é a motivação desta propriedade dentro da classe Ato.

## Troca para novo relator

- A troca para novo relator recebida pelo SCP-Sessões, define o campo NovoRelatorID na tabela dbo.Atos
- Com isso, o que era manifestação principal do relator anterior passa a ser uma 'manifestação por escrito' e ato fica temporariamente sem uma manifestação principal.
- Uma solicitação de alteração é aberta para esse novo relator (com o DelegadoUserID) e ele se manifesta não pela tela de manifestação por escrito e sim pela tela de Alterar Dados do Ato.
- A tela de alteração de dados do ato tem inteligência de perceber que não existe uma manifestação principal cadastrada e com isso cria uma nova manifestação nesse caso ao invés de substituir.
- Também durante esse período sem manifestação principal, a ficha do ato não mostra a informação do Relatório/Voto

## Usuário está lotado corretamente
- Por muitas vezes, o sistema precisa verificar se o usuário está lotado em órgão que permite realizar a operação.
- O normal é que o usuário precisa estar lotado no gabinete do relator do ato.
- Porém, no caso de [Decisão monocrática da presidência](#decisão-monocrática-da-presidência), o usuário precisa estar lotado espeficicamente na GPA.

## Tipos de Manifestação
- São os tipos de manifestação possíveis que tem mapeamento direto com o eTCM.
- Ou seja, todo documento criado dentro do sistema de Atos tem um mapeamento nesta tabela que usará como base para cadastrar um documento dentro do eTCM.

| ManifestacaoTipoID | ManifestacaoTipo                             | Documento_CategoriaID | Documento_TipoID |
|--------------------|----------------------------------------------|-----------------------|------------------|
| 1                  | Relatório/Voto                               | 8                     | 1                |
| 2                  | Histórico/Decisão Monocrática                | 8                     | 2                |
| 3                  | Histórico/Despacho Monocrático               | 8                     | 3                |
| 5                  | Proposta de Relatório/Voto                   | 8                     | 5                |
| 6                  | Histórico/Decisão Monocrática da Presidência | 8                     | 8                |

## Validações sobre flags em Partes de Dispositivo

- Validação sobre a tag [Responsável]
  - Não é feita validação se o responsável é um órgão.
  - ...
- Validação sobre a tag [Prazo]
  - ...