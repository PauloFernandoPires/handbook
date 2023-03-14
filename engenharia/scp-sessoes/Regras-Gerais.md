### Detalhamento Legado

- Um detalhamento é legado quando está com a flag "Legado" marcada como true na tabela "dbo.Detalhamentos"

### Situações de um detalhamento

| SituacaoID | Descrição |
| --- | --- |
| 1  | [Rascunho](/engenharia/scp-sessoes/Regras-Gerais.md#situação-em-modo-rascunho) |
| 2  | Pré-Acórdão liberado para ser gerado |
| 3  | Pedido de geração de Pré-Acórdão realizado |
| 4  | Pré-Acórdão gerado |
| 5  | Aguardando Alterações |
| 6  | Acórdão liberado para ser gerado |
| 7  | Pedido de geração de Acórdão realizado |
| 8  | Detalhamento concluído |
| 9  | Pedido de descarte realizado |
| 10 | Aguardando Alteração Restrita |

### Situação em modo Rascunho
- Essa situação permite ao usuário alterar o detalhamento sem que as regras de validação da votação sejam disparadas. Ou seja, é permitido salvar o detalhamento praticamente com qualquer configuração. 
- Essa situação também envia para o SCP-Atos um comando para que:
  - Todas as solicitações pendentes sejam canceladas.
  - **IMPORTANTE:** A opção de 'Novo Relator' no ato é baseada na opção ainda em rascunho do detalhamento. Isso porque é o único local previsto no sistema para salvar essa informação. (Ver: [Troca de Relator do ato](/engenharia/scp-atos/Regras-Gerais.md#troca-para-novo-relator))
