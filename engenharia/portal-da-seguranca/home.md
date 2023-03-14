# Descrição

- Web Service criado para atender pesquisas realizadas pelo Portal de Segurança em dados do TCMRio.
- A ideia é disponibilizar informações de pessoas em processos julgados pelo Tribunal.
- O Portal da Segurança tem o intuito de descobrir se determinada pessoa tem ilícitos registrados em vários órgãos de todas as esferas (Receita Federal, Ministérios Públicos, Tribunais de Justiça, etc...)

# Arquitetura

- Projeto web service simples já que o sistema nasce com escopo bem pequeno.

# Regras

- O TCMRio não se preocupará nesse primeiro momento se a referência a um processo é de ilícito ou não. Somente apresentará todos os processos aos quais a pessoa está relacionada.
- Nossa base de dados é em sua grande maioria não amarrada a CPF ou CNPJ. Até 2020/2021, a única informação que tínhamos era o campo texto 'Nome do Interessado' da tabela 'Processo'. 
- Depois disso, foi criada uma estrutura de Pessoa no banco SCP_ETCM que começou enriquecer essa informação.