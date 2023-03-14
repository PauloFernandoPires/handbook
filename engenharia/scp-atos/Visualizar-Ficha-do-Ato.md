# Descrição

- É a tela principal do ato. Na qual é possível realizar uma série de ações.
- A tela em si tem uma validação pequena. Todos os botões de ação aparecem para o usuário e somente acionam sua validações quando são clicados. Isso foi uma escolha pelo time para aumentar a transparência das permissões ao invés de sumir com eles. 
- Essa questão de sumir com os botões aumentava muito a quantidade de chamados já que o usuário simplesmente não sabia o motivo de não poder executar uma ação. E a equipe de desenvolvimento era acionada só para simular a ação e dizer qual era o motivo.

# Validações

- Se o ato estiver em uma situação diferente de "Somente o Gabinete Pode Ver", qualquer usuário pode visualizar a ficha.
- Quando a situação tiver a flag "Somente o Gabinete Pode Ver" habilitada (atuamente, só a situação 'Em Elaboração'):
  - Se o Ato for um Despacho Monocrático da Presidência, somente usuário da GPA pode visualizar.
  - Se o Ato for qualquer um diferente de Despacho Monocrático da Presidência, o usuário precisa pertencer ao órgão do [Relator Atual do Ato](engenharia/scp-atos/Regras-Gerais#relator-atual-do-ato).

