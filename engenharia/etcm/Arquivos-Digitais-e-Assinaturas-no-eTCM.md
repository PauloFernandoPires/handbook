# Explicação geral sobre Arquivos Digitais

- O eTCM possui uma entidade básica chamada Container (tabela dbo.Containers) que possui algumas especializações:
    - Processos

    - Documentos

    - Remessas

    - Processos não registrados
    
- Um container pode conter vários arquivos (tabela dbo.Arquivos) e um arquivo pode estar relacionado a vários containers. Essa relação é estabelecida na tabela dbo.Containers_Arquivos.

- Um arquivo equivale a uma peça. Ou, mais objetivamente, equivale a um arquivo PDF. Logo, arquivo, peça, PDF ou DOC são sinônimos nesse contexto.
- Um arquivo pode sofrer revisão, que significa trocar seu conteúdo por outro arquivo PDF. Porém, a revisão não substitui fisicamente o arquivo anterior. É criada uma nova entrada na tabela dbo.Arquivos com o novo documento e a tabela dbo.Arquivos_Correntes faz o consolidado de revisões apontando qual é o ArquivoID mais recente nessa cadeia.
- A tabela dbo.Containers_Arquivos possui a coluna ArquivoID inicial. Portanto, para descobrir qual é o arquivo mais atual, é preciso relacionar com a tabela dbo.Arquivos_Correntes.
- A tabela Arquivo não possui o conteúdo de bytes do arquivo. Essa informação fica em uma outra tabela chamada dbo.Arquivos_ArquivosDigital. Essa relação é do tipo 1xN. Ou seja, um arquivo possui somente um arquivo digital mas um arquivo digital pode pertencer a N arquivos. Isso dá flexibilidade para reaproveitar o mesmo arquivo digital para vários arquivos cadastrados. Facilita, por exemplo a criação de memorando circulares que começam com o mesmo arquivo digital mas que podem, eventualmente, serem substituídos individualmente.
- Segue um SELECT de exemplo para identificar os arquivos de um Documento e como é a relação das tabelas explicadas acima:
  ```sql
  SELECT
  *
  FROM Containers_Arquivos ca
  INNER JOIN Arquivos_Correntes ac
  ON ac.ArquivoID = ca.ArquivoID
  INNER JOIN Arquivos a
  ON a.ArquivoID = ac.ArquivoID_Corrente
  INNER JOIN Arquivos_ArquivoDigital aa
  ON aa.ArquivoDigitalID = a.ArquivoDigitalID
  WHERE containerID = 2021686  
  ```
- A tabela Arquivos_ArquivoDigital foi elaborada para utilizar o [FILESTREAM do SQL Server](https://docs.microsoft.com/en-us/sql/relational-databases/blob/filestream-sql-server).

# Explicação geral sobre Assinaturas
- Uma assinatura (tabela dbo.Arquivos_Assinaturas) essa relacionada a um arquivo. E um arquivo pode conter várias assinaturas.

- Para manter uma estrutura semelhante a de arquivos. a tabela dbo.Arquivos_Assinaturas não guarda o arquivo P7S da assinatura. Esse arquivo é armazenado em outra tabela chamada dbo.Arquivos_Assinaturas_ArquivoDigital.

- A tabela dbo.Arquivos_Assinaturas_ArquivoDigital não guarda seus dados usando FILESTREAM.

# Arquivo Digital e Assinaturas em storages externos
- Estamos em um momento de transição no qual os arquivos do eTCM passarão a ser armazenados em ambiente externo. Como, por exemplo, o Amazon S3 e o File Server no TCMRJ.

- Esse documento não cobrirá como isso será realizado. Mas a ideia é que, de tempos em tempos, os arquivos serão migrados do banco do eTCM para esse storage interno mantendo a referência de cada local. 

- Essa referência será armazenada em tabelas do banco SCP_ETCM e PORTAL_ETCM com o schema **nuvem**.

# Busca pelo conteúdo do arquivo digital ou assinatura
- A busca pelo conteúdo é realizada dentro das classes de contexto:
  - EtcmContext

  - PortalContext

  - RemessaContext

- Considerando que o arquivos podem estar em vários lugares diferentes (ex: bancos SCP_ETCM, PORTAL_ETCM, SCP_ETCM_ARCHIVE e PORTAL_ETCM_ARCHIVE, Amazon S3 e File Server), os contextos têm a inteligência de montar uma lista de file providers que tentarão, em ordem de prioridade, buscar o arquivo. Ou seja, caso a pesquisa apresente problema em um file provider, ele tentará o próximo da lista.

- A primeira decisão sobre a escolha da ordem de preferência é sobre a data de criação do documentos. Atualmente, se a data de criação tiver mais de 10 dias corridos em relação a data atual, a ordem de busca passará a priorizar da seguinte forma:
  - S3, File Server, Archive, Banco do Sistema.

- Caso contrário, esse arquivo é considerado novo e a ordem será:
  - Banco do Sistema, S3, File Server, Archive.

# Busca por Stream ou Bytes
- A busca pode ser feita pelo stream do arquivo ou diretamente pelos bytes. 

- Exemplos de situação da escolha de opção pelo stream:
  - API de download de arquivos utilizado pelo visualizador do eTCM

- Exemplos de situação da escolha de opção pelos bytes:  
  - Aplicativos Desktop pois o SQL FILESTREAM não aceita conexões de banco que não sejam com Windows Integration.

  - Download de assinaturas

