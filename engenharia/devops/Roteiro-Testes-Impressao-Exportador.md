# Roteiro para testar o Impressão App e Exportador de Peças (VisualStudio)

Para testar o IMPRESSÂO APP é necessário abrir o aplicativo no Visual Studio (propriedades do projeto) passando a matrícula de um usuário da secretaria das sessões (ex:902029) e o modo de debug (2). Eu costumo usar a matricula da chefe do setor.

Exemplo nas propriedades do projeto ImpressaoAPP setar:

```
902029 debug
```

O IMPRESSAO APP é parecido com o ASSINADOR (no sentido de quê possui um menu de contexto pra visualizar a peça) e seus pontos de entrada de testes são o botão de imprimir e a opção de visualização no menu de contexto.

Já pra o EXPORTADOR DE PEÇAS precisa utilizar uma dinâmica com a tabela app.Token para testar.
Primeiro, pra gerar um token acessamos qualquer gerador de GUID online, depois substituimos o GUID no SQL abaixo para o TOKEN ficar na base de dados e conseguirmos testar:

```sql
USE SCP_ETCM
GO

--apaga token para reuso
SELECT * FROM app.Token as t WHERE t.GUID like 'AAE19FE7%'

DELETE FROM SCP_ETCM.app.Token WHERE GUID='AAE19FE7-77FC-41E7-A5DF-0247C847865B'
--insere token
INSERT INTO SCP_ETCM.app.Token
    (GUID, DataHora, UserID, AcaoID, URL, UserIP, Path, ContainerID, TipoExportacao)
VALUES
    ('AAE19FE7-77FC-41E7-A5DF-0247C847865B',
     GetDate(),
     991699,
     3,
     '',
     '10.5.16.114',
     'C:\tmp\',
     1838804,
     2
     )
     
--Mostra os tokens mais recentes
  SELECT top 5 *
  FROM [SCP_ETCM].[app].[Token]
  where AcaoID = 3
  order by DataHora desc
```

por ultimo, basta rodar o EXPORTADOR passando o GUID que você quer EXPORTAR e o modo de exportação (3)

Exemplo nas propriedades do projeto ExportadorAPP setar:

```
AAE19FE7-77FC-41E7-A5DF-0247C847865B 3
```