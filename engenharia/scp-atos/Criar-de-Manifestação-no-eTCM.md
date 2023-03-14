# Descrição

- É uma comunicação via API com o eTCM para criação de manifestação.

# Validações
- Não permite a criação se houver na  tabela dbo.Atos_Manifestacoes outra manifestação com o mesmo:
  - Número
  - Ano
  - [Tipo de Manifestação](/engenharia/scp-atos/Regras-Gerais#tipos-de-manifestação)
  - UserID do Conselheiro

# Fluxo
- O retorno da criação devolve o ContainerID criado que será usado para cadastrar a manifestação dentro do sistema.