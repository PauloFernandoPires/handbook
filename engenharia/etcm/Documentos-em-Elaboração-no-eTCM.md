# Explicação geral sobre Documentos em Elaboração

- A funcionalidade foi criada para permitir ao usuário vincular um DOCX a um processo antes que ele seja efetivamente autuado no processo. A ideia é que ele seja um documento que possa ser substituído várias vezes até que tenha uma versão final que pode ser autuada ao processo como um PDF.


# Procedimento técnico de criação

- A criação do Documento não o autua diretamente ao processo. É criado um documento independente com um vínculo exclusivo para o Processo.
- O documento é criado da mesma forma que qq outro documento PDF. A única diferença é que o arquivo associado é um Word.
- Sobre as assinaturas, elas são criadas com a flag **Disponivel = 0** na tabela **Arquivos_Assinaturas**. Isso é para evitar que o usuário assine o documento word ao invés do PDF definitivo. Além disso, a assinatura não aparecerá pendente para o usuário na mesa de trabalho.


# Procedimento técnico de autuação
- Em algum momento, o documento Word estará finalizado e será autuado no processo. 
- No momento da autuação, os seguintes procedimentos são realizados.
  - Todas as assinaturas são liberadas marcando a flag **Disponivel = 1** na tabela **Arquivos_Assinaturas**
  - O arquivo PDF gerado pelo Spire a partir do DOC ocupará o espaço do arquivo digital atual. Ou seja, os identificadores de ArquivoID e ArquivoDigitalID do PDF serão os mesmos do DOC original.
  - O nome do arquivo na tabela **Arquivos** será atualizado de .doc(x) para .pdf.
  ```sql
  ArquivoID   NomeArquivo      
  antes------ -----------------
  1447536     DOC_00.docx      
  depois------ -----------------
  1447536     DOC_00.pdf       
  ```
  - O arquivo DOC será migrado para uma nova entrada na tabela **Arquivos_ArquivoDigital** com um novo ArquivoDigitalID.
  - O ArquivoDigitalID mais antigo (que passou a ser do PDF) terá atualizado o campo **ArquivoDigitalOriginalID** para guardar relação com o arquivo DOC.
  ```sql
  ArquivoDigitalID MimeTypeID ArquivoDigitalOriginalID Temporario Replicavel 
  antes----------- ---------- ------------------------ ---------- ---------- 
  890137           3          NULL                     1          0          
  depois---------- ---------- ------------------------ ---------- ---------- 
  890137           1          890138                   0          1          
  890138           3          NULL                     0          0          
  ```
