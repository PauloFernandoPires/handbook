O smoke test tem a intenção de ser realizado em ambiente de HML para identificar se o sistema se apresenta utilizável antes de uma publicação para produção. Não tem a intenção de ser um teste aprofundado do sistema pois isso deve ser realizado em momento antecedente. 

Maiores detalhes sobre o que é smoke test. : https://pedrohjmartins.medium.com/smoke-testing-dfcd62903648

Seguem baixo sugestões de roteiro de smoke tests. É claro que, dependendo da nova funcionalidade que será publicada, o teste pode ser um pouco diferente para verificar se o sistema está estável para publicação.

# Roteiro padrão de Smoke Test para publicação do SCP - eTCM

- Entrar no eTCM e criar um ofício que será enviado para órgão externo.
- Assinar o ofício, enviar o mesmo para órgão externo.
- Receber o ofício pelo Portal do Jurisdicionado.
- Criar uma remessa de resposta no Portal do Jurisdicionado e enviá-la para o eTCM.
- Receber a remessa no eTCM e enviar para o departamento de protocolo.
- Entrar com usuário do protocolo no eTCM e receber a remessa.
- Com o mesmo usuário de protocolo, acessar o SCP e criar um processo de aposentadoria.
- Ao final da criação de um processo de aposentadoria, autuar a remessa ao processo.
- Por fim, visualizar o processo pelo visualizador do eTCM.

# Roteiro padrão de Smoke Test para publicação de SCP-Atos

- Associar o usuário que será utilizado como teste em algum gabinete de conselheiro.
- Usar esse esse gabinete para criar uma minuta de acórdão.
- Criar a minuta até o final (dispositivos, considerações finais, etc...)
- Acessar o preview do acórdão para ver se foi gerado.

# Roteiro padrão de Smoke Teste para publicação de SCP-Sessões

- Entrar em alguma sessão que esteja aberta.
- Caso tenha alguma sessão ordinária aberta, alterar o detalhamento de forma que precise acessar o SCP-Atos para criar alguma solicitação.
  - Entrar no SCP-Atos para concluir a alteração (isso precisa atualizar a situação do detalhamento no SCP-Sessões)
- Caso não tenha sessão ordinária aberta, entrar em uma sessão virtual, realizar algumas alterações na tela de detalhamento e salvar. 
- É importante remover do detalhamento no modo rascunho para que o sistema realize mais validações.

