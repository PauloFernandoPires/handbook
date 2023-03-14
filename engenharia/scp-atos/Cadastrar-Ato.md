# Descrição

- Usuário deseja cadastrar um novo ato.
- O ato pode ter várias [naturezas](/engenharia/scp-atos/Regras-Gerais#naturezas-de-um-ato).

# Primeiro passo - A escolha do processo
- Nesse primeiro passo, o usuário escolhe o processo inicial que será referência para a criação do ato.
- O relator e possível relator substituto deste processo servirão de base para criação do ato e várias das suas validações.
- Essa tela só verifica se o processo digitado existe, após essa validação, ele é direcionado para o segundo passo que é o cadastro em si.

# Segundo passo - Cadastro do Ato
- Essa tela apresenta o formulário de cadastro

# Segundo passo - Validações no Carregamento da Tela
- Já no carregamento da tela, algumas validações importantes são realizadas. São causas de bloqueio do cadastro:
  - Se existe algum ato em aberto **não processado** para o processo.
  - Se o processo for um apenso de outro.
  - Se o processo tem relator.
  - Se o usuário está [lotado corretamente para executar a ação](/engenharia/scp-atos/Regras-Gerais#usuário-está-lotado-corretamente).

# Segundo passo - Validações e fluxo no submissão do formulário
- Verifica se os apensos escolhidos pertencem ao processo em consulta ao SCP-API.
- Em decisão monocrática:
  - Escolhe como relator do ato o Presidente em Exercício do Tribunal
  - Faz a validação de PodeCriar baseado nesta informação.
  - Se o usuário está [lotado corretamente para executar a ação](/engenharia/scp-atos/Regras-Gerais#usuário-está-lotado-corretamente).
  - O órgão de criação da manifestação será GPA.
- Em qualquer outra natureza:
  - Escolhe como relator e relator substituto o mesmo do processo inicialmente selecionado.
  - Faz a validação de PodeCriar baseado nesta informação.
  - Se o usuário está [lotado corretamente para executar a ação](/engenharia/scp-atos/Regras-Gerais#usuário-está-lotado-corretamente).
  - O órgão de criação da manifestação será o gabinete do **relator do processo**.
- Se o ato for uma minuta de acórdão e tiver um relator substituto associado, o tipo de manifestação do ato é um **Proposta de Relatório/Voto**. Caso contrário, é um **Relatório/Voto**.
- O SCP-Atos enviará para o eTCM os dados para [criação do manifestação](/engenharia/scp-atos/Criar-de-Manifesta%C3%A7%C3%A3o-no-eTCM).


