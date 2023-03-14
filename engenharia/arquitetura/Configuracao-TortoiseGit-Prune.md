O Tortoise Git, com o passar do tempo, vai mantendo uma lista grande de branches que não existem mais no gitlab e começa a ficar chato procurar os branches que realmente existem. Isso acontece porque, por padrão, o Tortoise não faz um 'Prune' no ambiente local dos branches que não existem mais no server.
(Se o branch existe efetivamente na sua máquina local, mesmo que não exista no servidor, ele não apaga automaticamente. Ainda precisa entrar no repositório local para apagar o branch que vc não está mais utilizando.)

Tem duas forma de resolver isso. Uma é: cada vez que vc fizer um pull, pode marcar um checkbox 'Prune' para fazer essa 'sincronia'. 

A outra (que eu fiz) é: Dentro de Tortoise Git -> Settings, escolher a opção 'Global' e marcar o checkbox 'Prune'. Com isso, essa opção marcada vira a padrão para qualquer Pull realizado na sua máquina, em todos os repositórios. 

![TortoiseGit-Prune](uploads/b548526ebb8e79b77ceaaa35f40c8c12/TortoiseGit-Prune.PNG)