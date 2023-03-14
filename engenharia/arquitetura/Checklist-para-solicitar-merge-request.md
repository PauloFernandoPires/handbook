Seguem os pontos que precisam ser analisados em qualquer merge request pelo desenvolvedor de forma a facilitar o trabalho do revisor e evitar retrabalho.

# Itens obrigatórios para verificação pelo desenvolvedor
- Resolver warnings do Stylecop.
- Resolver messages do Code Analysis.
- Rodar testes unitários e todos finalizarem com sucesso.
- Antes de cada commit, revisar o que está sendo submetido para verificar se realmente faz sentido com o que está sendo *commitado*. Fazer a mesma validação depois de criar o merge request que é a consolidação de todos os commits do trabalho. Exemplos de coisas que podem acontecer:
  - Inclusão ou Atualização de pacotes Nuget desnecessários.
  - Inclusão de arquivos desnecessários.
  - Inclusão de chaves de configuração denecessárias.
  - Remoção de arquivo de imagem pelo Windows Explorer sem remover do projeto dentro do Visual Studio (isso dá problema em projetos .NET Full Framework quando são compilados no Jenkins)
- Dentro do Merge Request, adicionar comentários com as seguintes informações:
  - Prova de que a funcionalidade está OK (Imagem, Vídeo ou Resultado de Consulta do SQL)
  - Um roteiro de teste simplificado para ajudar o revisor. Exemplos de coisas que podem estar descritas:
    - Descrição sucinta da alteração
    - Código de SQL para procurar exemplos de entidades
    - Caminho feliz
    - URL da tela
    - Expectativa de resultado
    - Validações que podem ser realizadas
  - Nem todos os itens acima precisam necessariamente ser descritos. Dependendo da complexidade da funcionalidade, pode ser que não seja necessária tanta informação.