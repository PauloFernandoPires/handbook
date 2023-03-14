# Descrição

- O usuário deseja consultar um chamado.
- Existe vídeo de treinamento localizado em: 
  - G:\DESENVOL\Treinamento\2023-03-08 - Ouvidoria - Abrir chamado no WebApp
  - G:\DESENVOL\Treinamento\2023-03-08 - Ouvidoria - Funcionamento de aplicação VB

# Validações 

- O número do chamado precisa existir.
- O código de controle precisa bater com o cadastrado. (São os primeiros 4 caracteres da coluna 'Verificador' na tabela **PORTAL_ETCM.ouvidoria.Chamados_WebApp**)

# Fluxo

- Além da consulta do banco PORTAL_ETCM. Existem views no mesmo banco que refletem o banco OUVIDORIA.
- Com isso, o usuário consegue mais informações de retorno do chamado.
- Essa views no banco PORTAL_ETCM estão com o schema **ouvidoria**.