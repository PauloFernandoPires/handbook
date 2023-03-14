# Descrição

- Esse é um pedido realizado pelo SCP que insere na tabela dbo.Fila uma ação para criar um documento de distribuição. 

- É uma situação na qual o SCP automaticamente distribui o processo para um relator e precisa adicionar uma peça ao processo informando que o relator for determinado.

- O campo AcaoID é 3 (Gerar PDF da Distribuição Eletrônica)

- O documento é criado dinamicamente em PDF usando a ferramenta iTextSharp.