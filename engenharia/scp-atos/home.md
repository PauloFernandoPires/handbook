# Funcionalidades

- [Cadastrar Ato](./Cadastrar-Ato)
- [Cadastrar Parte de Dispositivo](./Cadastrar-Parte-de-Dispositivo)
- [Excluir Ato](./Excluir-Ato)
- [Visualizar Ficha do Ato](./Visualizar-Ficha-do-Ato)

# Conceitos

* [Regras Gerais](./Regras-Gerais)
* [Alteração Restrita](../scp-sessoes/Alteração-Restrita)

# Glossário

### Manifestação por Escrito
- São manifestações de conselheiros não relatores que acompanham o ato.
- Tanto manifestações por escrito quanto a manifestação principal são cadastradas na tabela dbo.Atos_Manifestacoes. A determinação sobre qual é a principal depende de quem é o [manifestante principal](#manifestante-principal).

### Manifestante Principal
- Todo conselheiro que tem um voto cadastrado para um ato é manifestante. Porém o manifestante principal é o voto do conselheiro que está no papel de relator em determinado momento. Então, pode ser o RelatorID, RelatorSubstitutoID ou NovoRelatorID que estão cadastrados na tabela dbo.Atos para um ato específico. 
- A ordem de preferência é: NovoRelatorID > RelatorSubstitutoID > RelatorID.
- As outras manifestações cadastradas para um ato são chamadas 'Manifestações por escrito'

### Dispositivo e Parte de Dispositivo

- O Dispositivo é o conjunto de partes de decisões objetivas sobre um ato. 
- Uma **Parte de Dispositivo** contém:
  - Processo relacionado (que precisa fazer parte do Ato)
  - Comando
  - Prazo (se o comando obrigar)
  - Texto (que será colocado no acórdão)
  - Responsável (PJ, PF ou Pré-Cadastro)
- O sistema começou com o conceito de que o usuário cadastrava um dispositivo. Por isso, em código, as funcionalidades podem ter nomes nos quais fica parecendo que ele está cadastrando um dispositivo inteiro. Mas isso não existe. O usuário cadastra **partes de dispositivos**. A ficha do ato é que consolida dessas partes em um **dispositivo** completo que tem uma **decisão** que a junção de todos os comandos selecionados.