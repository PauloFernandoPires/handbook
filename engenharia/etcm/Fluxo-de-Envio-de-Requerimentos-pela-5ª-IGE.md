# Descrição

Esse é o procedimento no qual a 5ª IGE automaticamente enviar requerimentos para os jurisdicionados para que sejam enviados dados para análise de aposentadorias e pensões.

# Fluxo

- 5ª IGE envia um requerimento pelo sistema de Integração eTCM -> Portal para gerar esse documento lá no IPLAN
  - Esse entrada é pela procedure **SCP_ETCM.dbo.sp_FilaDoc_IncluirRequerimento**
  - Se o usuário usar o eTCM para assinar o requerimento, é enviada uma mensagem para a fila de RabbitMQ para criar o documento dentro do Portal do Jurisdicionado
  - Se o usuário usar o Assinador para assinar, é enviado um pedido para o Manutenção através da tabela Fila para que seja incluída uma mensagem no RabbitMQ.
    - Esse segundo fluxo é mais quebrado pois o Assinador ainda funciona em .NET 4.5 e essa versão do framework não é compatível com MassTransit e RabbitMQ. Já o Manutencão está desenvolvido em .NET 4.8.
- Jurisdicionado responde requerimento com uma remessa.
- 5ª IGE controla as remessas em sistema próprio distribuindo entre seus auditores.
- Auditor entrar no Portal do Jurisdicionado e aceita a remessa.
- Portal do Jurisdicionado envia remessa para a 5ª IGE dentro do ambiente do eTCM
- Serviço de integração cria remessa no banco SCP_ETCM e coloca para a 5ªIGE receber.
- Existe um job no banco chamado **SiCAP Portal eTCM** que realiza os seguintes procedimentos
  - Recebe automaticamente as remessas na 5ª IGE.
  - Cria processos associados a remessa usando a procedure **SCP_ETCM.dbo.sp_IntegracaoSAC_CriarProcessoEletronico**
- Depois da criação do processo, o SICAP faz um pedido para a autuar a peça dentro do processo através da integração do FilaDoc.