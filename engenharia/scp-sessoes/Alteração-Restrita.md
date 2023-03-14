# Descrição

- A funcionalidade foi criada para permitir ao usuário alterar alguns dados do ato DEPOIS que ele já foi processado.
- Permite trocar:
  - O arquivo PDF do voto do manifestante principal
  - O texto de parte de um dispositivo
  - O responsável pela parte do dispositivo.
  - Considerações finais
  
- Logo, não permite alterar:
  - Número e Ano da manifestação
  - Remover ou incluir dispositivos
  - Alterar processos relacionados
  - Dentro de uma parte de dispositivo, não permite também alterar processo relacionado e comando.


# Fluxo para Minuta de Acórdão
- Dentro do sistema SCP-Sessões, um detalhamento de votação mostrará o botão para liberar ação restrita quando:
  - O *detalhamento* está na situação [Detalhamento Concluído](./Regras-Gerais#situações-de-um-detalhamento)
  - O usuário precisa ter a permissão: **Ficha_do_Detalhamento_da_Votacao.CanSpecial2**
- Ao confirmar a liberação, o sistema SCP-Atos troca a situação do *Ato* para **Liberado para Alteração Restrita** (SituacaoID = 6) e o sistema SCP-Sessões troca a situação do *detalhamento* para 'Aguardando Alteração Restrita' (SituacaoID = 10)
- É criada uma solicitação em aberto para o relator atual do ato na tabela SCP_ATOS.dbo.Atos_Solicitacoes para que ele possa realizar sua alteração e tenha um controle de conclusão.
- Ao concluir a solicitação, o *Ato* volta para a situação 'Fechado para alteração' (SituacaoID = 99) e notifica o SCP-Sessões da conclusão.
- No SCP-Sessões, o detalhamento volta para a situação [Detalhamento concluído](./Regras-Gerais#situações-de-um-detalhamento) quando o resultado da votação for [Pedido de Vista](#) ou [Retirada de Pauta](#). Já para os outros resultados o detalhamento volta para situação [Acórdão liberado para ser gerado](./Regras-Gerais#situações-de-um-detalhamento)
- Ao colocar o detalhamento na situação 'Acordão liberado para ser gerado', permite ao usuário gerar novamente o acórdão com as modificações realizadas pelo Gabinete.

# Fluxo para Atos Monocráticos
- O botão de liberar alteração restrita será disponibilizado no SCP, na tela de Cadastro de Ato Monocrático, apenas para usuários da SES.
- A Tabela 'Naturezas' no SCP-Atos possui uma propriedade chamada "TemDetalhamentoAssociado", que será _true_ apenas para Minuta de Acórdão. O sistema SCP-Atos, na conclusão da alteração restrita, analisa essa *flag* e, no caso de _false_ (Atos Monocráticos), não irá disparar notificação para o Detalhamento em SCP-Sessões (API do Atos), visto que esse tipo de ato não possui detalhamento no SCP-Sessões.