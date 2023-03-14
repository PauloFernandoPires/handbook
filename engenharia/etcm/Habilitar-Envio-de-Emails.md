# Descrição

- Os serviços web instalado no IPLAN não se utilizam do MailQueue pois não temos uma conexão permitida. 
- Poderíamos fazer uma solução via RabbitMQ ou replicação de banco mas isso não foi realizado.
- Então, o Portal do TCMRio e o Web App acessam direto um servidor de e-mail para envio de mensagens.
- Para evitar que em ambientes de Desenvolvimento sejam enviados e-mails indesejados, existe uma flag em cada site que determina se o e-mail será enviado ou não.
```xml
<!-- Portal do Jurisdicionado - web.config -->
  <appSettings>
    ...
    <add key="HabilitarEnvioDeEmailDeNotificacao" value="false" />
    ...
  </appSettings>

<!-- WebApp - web.config -->
  <appSettings>
    ...
    <add key="HabilitarEnvioDeEmail" value="false" />
    ...
  </appSettings>
```
- Essa flag fica desabilitada por padrão em todos os ambientes, EXCETO PRD.
- Então, para simular o envio de e-mail, precisa colocar manualmente como true. 
- Como sugestão, use seu e-mail pessoal nos formulário de cadastro para evitar o envio indevido para terceiros.