# Roteiro Testes Nuvem


**<span style="text-decoration:underline;">Testes sobre eTCM - Memorando</span>**



* Criação de memorando com assinaturas pendentes (Paulo, Augusto)
* Teste ainda sem nenhuma execução de migração de archive ou nuvem.
    * eTCM 
        * Pelo visualizador.
        * Exportação de PDF único (carimbado).
    * Assinador 
        * Pelo download de peça (opção de exportar peça)
* Realizar migração para archive (SCP_ETCM_ARCHIVE) de arquivo digital
* Realizar purge do SCP_ETCM
    * Mesmos testes acima para ver se pega o archive
* Realizar migração para nuvem
* Realizar purge do archive
    * Mesmos testes acima (vai pegar da nuvem)
* Realizar assinatura do documento (Paulo) pelo assinador
* Realizar assinatura do documento (Augusto) usando SERPRO e upload de P7S
    * Realizar teste de download de arquivo de assinatura pelo eTCM
    * Testar no validador do eTCM e da ITI
* Realizar migração para archive de arquivo de assinatura
* Realizar purge do etcm SCP_ETCM
    * Realizar teste de download de arquivo de assinatura pelo eTCM (deve pegar do archive)
    * Testar no validador do eTCM e da ITI
* Realizar migração para nuvem
* Realizar purge do archive (SCP_ETCM_ARCHIVE)
    * Realizar teste de download de arquivo de assinatura pelo eTCM (deve pegar da nuvem)
    * Testar no validador do eTCM e da ITI

**<span style="text-decoration:underline;">Testes sobre eTCM - Peça autuada em processo</span>**



* Criar peça em elaboração em um processo. (DOCX)
* Autuar peça em elaboração em processo. (Vira PDF)
* Teste ainda sem nenhuma execução de migração de archive ou nuvem.
    * eTCM 
        * Pelo visualizador.
        * Exportação de PDF único (carimbado).
        * Na tela do hub, download de peça original.
    * Portal
        * Pelo visualizador.
        * Exportação de PDF único.
* Realizar migração para archive (SCP_ETCM_ARCHIVE) de arquivo digital em HML
* Realizar migração para archive (SCP_ETCM_ARCHIVE) de arquivo digital em HMLINTERNET
* Realizar purge do SCP_ETCM em HML
    * Mesmos testes acima para ver se pega o archive 
* Realizar migração para nuvem
* Realizar purge do archive (SCP_ETCM_ARCHIVE) em HML
* Realizar purge do archive (SCP_ETCM_ARCHIVE) em HMLINTERNET
    * Mesmos testes acima (vai pegar da nuvem)
* Testar o mesmo procedimento para o arquivo original. Ou seja, migrar aos poucos para ver se ele pode ser resgatados de todos os locais

**<span style="text-decoration:underline;">Testes sobre eTCM - Ofício</span>**



* Criação de ofício com assinatura pendente.
* Realiza a assinatura.
* Exportar para o Portal (via serviço de integração)
* Recebe ofício no Portal
    * Teste de visualização de documento no portal.
    * Teste de download do P7S no portal. (criar issue caso não tenha)
* Realizar migração para archive (SCP_ETCM_ARCHIVE) de arquivo digital e assinatura em HML
* Realizar migração para archive (SCP_ETCM_ARCHIVE) de arquivo digital e assinatura em HMLINTERNET
* Realizar purge do SCP_ETCM em HML
    * Mesmos testes acima para ver se pega o archive
* Realizar migração para nuvem de arquivo e assinatura.
* Realizar purge do archive (SCP_ETCM_ARCHIVE) em HML
* Realizar purge do archive (SCP_ETCM_ARCHIVE) em HMLINTERNET
    * Mesmos testes acima (vai pegar da nuvem)

**<span style="text-decoration:underline;">Testes sobre Portal - Criação de remessa</span>**



* Criar Remessa com assinaturas como resposta do ofício criado acima
* Realizar aprovação e enviar para órgão interno
* Receber remessa no eTCM
* Testes
    * No Portal:
        * Visualizar peças da remessa
        * Visualizar assinaturas da remessa
    * No eTCM:
        * Visualizar peças no visualizador
        * Realizar exportação de PDF único
        * Visualizar assinaturas 
* Realizar migração para archive (PORTAL_ETCM_ARCHIVE) de arquivo digital e assinaturas em HMLINTERNET
* Realizar migração para archive (PORTAL_ETCM_ARCHIVE) de arquivo digital e assinaturas em HML
* Realizar purge no PORTAL_ETCM em HMLINTERNET
    * Mesmos testes acima para ver se pega o archive
* Realizar migração para nuvem de arquivos e assinaturas (apontando para HMLINTERNET)
* Realizar purge no PORTAL_ETCM_ARCHIVE em HMLINTERNET
* Realizar purge no PORTAL_ETCM_ARCHIVE em HML
    * Mesmos testes acima para ver se pega da nuvem

**<span style="text-decoration:underline;">Testes sobre o Exportador </span>**



* Autuar a remessa recebida acima ao processo que teve peça autuada.
* Abrir o SCP e executar o exportar para esse processo.

**<span style="text-decoration:underline;">Testes sobre o Inteiro Teor</span>**



* Se for o caso, forçar a disponibilização no inteiro teor
    * Forçar peça pública (fase 0) em HML
        * A fase 0 precisa ser a máxima + 1 pois o select que busca os arquivos nunca pega os arquivos da última fase.
    * Atualizar container do processo em SCP_InteiroTeor.dbo.InteiroTeor_Processos com situação 0 para liberar em HML
* Pegar o mesmo caso usado no Exportador

**<span style="text-decoration:underline;">Testes sobre Impressão</span>**



* Entrar na aplicação com usuário de Sessões (ex: 902019)
* Procurar o ArquivoDigitalID de um ofício que esteja na fila (e seu AssinaturaArquivoID)
* Testes
    * Testar impressão
    * Testar download em menu ‘opções’
* Realizar migração para SCP_ETCM_ARCHIVE do arquivo e da assinatura
* Realizar purge no SCP_ETCM
    * Mesmos testes acima para ver se pega o archive
* Realizar migração para nuvem
* Realizar purge no SCP_ETCM_ARCHIVE
    * Mesmos testes acima para ver se pega da nuvem

**<span style="text-decoration:underline;">Testes sobre eTCM - sobre o memorando</span>**



* Testar juntada de memorando a outro documento.
* Testar substituição/correção de peça do memorando.
* Testar para arquivo incluído em comentário de correção.