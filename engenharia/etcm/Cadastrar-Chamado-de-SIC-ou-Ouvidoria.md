# Descrição

- O usuário deseja abrir um chamado.
- Existe vídeo de treinamento localizado em: 
  - G:\DESENVOL\Treinamento\2023-03-08 - Ouvidoria - Abrir chamado no WebApp
  - G:\DESENVOL\Treinamento\2023-03-08 - Ouvidoria - Funcionamento de aplicação VB

# Validações 

- Dados pessoais são obrigatórios.
- Tipo do Chamado é obrigatório.
- Recado é obrigatório.
- Limite de 5 arquivos por solicitação.
- Se o tipo de chamado (chamado de Categoria dentro do sistema) tiver a propriedade 'Requer_Pai', é obrigatório informar o número do chamado pai. Esse tipo de chamado é usado na opção de SIC para o cidadão pedir revisão de uma informação que não foi concedida. A view é **PORTAL_ETCM.ouvidora.Chamados_Categorias** e a coluna é **Requer_Pai**.

# Fluxo

- Ao salvar o chamado, os dados são armazenados em: 
  - **PORTAL_ETCM.ouvidoria.Chamados_WebApp**
  - **PORTAL_ETCM.ouvidoria.Chamados_WebApp_Arquivos**
- A tela seguinte mostrará um número de chamado e um código de controle que o usuário deve guardar para conseguir consultar o andamento do chamado.
- O banco PORTAL_ETCM é replicado para o ambiente interno e o sistema VB de Ouvidoria passa a ler os novos chamados para serem tratados.
