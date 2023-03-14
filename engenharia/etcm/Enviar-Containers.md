# Descrição

- O usuário deseja tramitar um documento ou remessa para outro órgão.
- Essa feature tem um chaveamento no CommandValidator para pegar regras de validação diferentes entre containers (documentos ou remessas) no eTCM ou remessas no sistema do Portal.

# Validações no caso de documento ou remessa no eTCM

- Precisa de órgão origem.
- Precisa de órgão destino.
- Precisa de usuário executor da ação.
- Precisa pelo menos um container selecionado.
- Usuário precisa de permissão de envio (AppResource 106) e no órgão de origem.
- Nenhum container selecionado está em trânsito.
- Nenhum container selecionado tem correção em aberto no órgão da carga.
- Nenhum container selecionado tem vínculo exclusivo.
- Se o envio for executado pela tela do eTCM, todos os containers precisam estar na carga de um órgão do qual o usuário executor faz parte.
  - Ou seja, a regra acima não cabe para o serviço de integração que cria um ponteiramento de remessa e já envia para o órgão interno do eTCM.
- Se for órgão externo:
  - Usuário precisa de permissão de envio (AppResource 122) e no órgão de origem.
  - O container precisa ser um documento. 
  - O documento precisa ter em sua configuração o campo Localizacao igual a "E". Ou seja, pode ser enviado para órgão externo.
  - O documento não pode ter nenhum vínculo ativo.
  - O documento não pode ter sido enviado para fora anteriormente. Ou seja, ele só pode ser enviado para fora uma única vez.
  - O órgão externo de destino precisa ter pelo menos um usuário associado. (Isso é uma consulta no banco PORTAL_CSLIB_UserManager procurando por usuários no OrgaoID nos grupos 20 (Gestor), 21 (Delegado) e 22 (Padrão)).

# Validações no caso de remessa no Portal

- Precisa de órgão origem.
- Precisa de órgão destino.
- Precisa de usuário executor da ação.
- Precisa pelo menos um container selecionado.
- Usuário precisa de permissão de envio (AppResource 106) e no órgão de origem.
- Nenhum container selecionado está em trânsito.
- Nenhum container selecionado tem vínculo exclusivo.
- Todos os containers precisam estar na carga de um órgão do qual o usuário executor faz parte.

# FAQ