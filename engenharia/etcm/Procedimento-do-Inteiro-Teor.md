# Explicação geral

- O usuário realizará o pedido pelo portal.
- O pedido é enviado para fila do RabbitMQ no modo **Fire e Forget** (sem aguardar retorno).
- A página que fez o pedido passa a mostrar uma barra de progresso e ela faz uma requisição AJAX de tempos e tempos para saber se os arquivos do processo já estão no banco do InteiroTeor no ambiente do PORTAL.

# Montagem de lista de processos

- A lista de processos disponíveis para download fica em SCP_InteiroTeor.dbo.InteiroTeor_Processos. Essa é a tabela que será consultada para permitir realizar o pedido ou não. Flags importantes:
  - Situacao: 
    - 0 = Disponível para solicitar Inteiro Teor
    - Outros códigos = Vários motivos que não permitem o download.
  - Download_Disponivel: 
    - Se igual a 1, o download já foi realizado e se encontra no banco SCP_InteiroTeor.
- Essa tabela é atualizada todo dia a partir de um job em banco de dados atráves da procedure **SCP.dbo.sp_InteiroTeor_CarregaProcessos** no servidor TCMBD1.

# Limpeza do banco do Inteiro Teor

- Para limpar o banco e diminuir seu tamanho, deve-se executar a procedure **SCP_InteiroTeor.dbo.sp_LimpezaInteiroTeorDeProcesso** no servidor TCMBD1.
- A limpeza remove os pedidos de mais de 7 dias.
- A limpeza no banco do servidor TCMBD1 replicará a remoção no servidor de banco de dados no Portal.

# A solicitação e cópia dos arquivos em mais detalhes.

- O pedido realizado no site do Portal é inserido na fila **(ha.solicitacao-inteiroteor)** do RabbitMQ do servidor do IPLAN.
- O serviço **Tcmrj.Etcm.Services.InteiroTeor** localizado em servidor interio pega a pedido com o ContainerID do processo desejado.
- O método *\eTCM\src\Tcmrj.Etcm.Services.InteiroTeor\Dal\RoboRepositorio.cs#RetornarArquivosETCM* é o que possui o SELECT para pegar os arquivos desejados.
- O SELECT possui as seguintes regras básicas:
  ```sql
  ...
   WHERE ca.ContainerID =  @containerID
        AND ca.Excluido = 0
          AND ca.Restricao = 0
        AND ca.Fase <= (
          SELECT MAX(Fase)
          FROM ETCM_Containers_Acessos AS cac
          WHERE cac.PerfilID = 0
            AND cac.ContainerID = ca.ContainerID
          )
        AND ca.Fase < (
          SELECT MAX(Fase)
          FROM ETCM_Containers_Acessos AS cac
          WHERE cac.ContainerID = ca.ContainerID
          )
        AND NOT EXISTS (
          SELECT *
          FROM ETCM_Arquivos_Assinaturas AS aa
          WHERE aa.ArquivoID = a.ArquivoID
            AND aa.DataHoraAssinatura IS NULL
          )
        AND p.Eletronico = 1
  ```
  - Peças não excluídas
  - Peças não restritas
  - Peças que tenham fase igual ou menor que fase do perfil público (perfilID = 0)
  - Peças que tenham fase menor que a maior fase do processo.
    - A explicação dessa regra é que o processo já tem sua atualização do perfil público no encerramento da sessão. Porém, o órgão das Sessões ainda está elaborando certidões e ofícios nesse momento e esses documentos ainda não devem ser expostos ao público.
    - Portanto, somente após a tramitação e recebimento desse processo para qualquer outro órgão, é que fase aumentada liberará as certidões e ofícios para o público.
- A busca pelo conteúdo dos arquivos segue o padrão da busca dos aplicativos Desktop e pode pegar de qualquer provider cadastrado (banco, archive, nuvem ou storage interno).
