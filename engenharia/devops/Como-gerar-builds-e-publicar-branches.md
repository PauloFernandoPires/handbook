Pode ser necessário gerar um build de uma versão diferente da master para publicá-la em DSV ou HML. Segue um exemplo abaixo para mostrar como isso deve ser feito.

## Exemplo de branch em subpasta 'Features'
- Nome do branch: **Features/S125.8-Alteração_AtosMonocráticos**
- No projeto de build, os campos devem ser preenchidos da seguinte forma:
  - VERSAO: **S125.8-Alteração_AtosMonocráticos**
  - GITPATH: **refs/heads/Features/**
- No projeto de publicação:
  - VERSAO: **S125.8-Alteração_AtosMonocráticos**

## Exemplo de branch em subpasta issues
- Nome do branch: **issues/324**
- No projeto de build, os campos devem ser preenchidos da seguinte forma:
  - VERSAO: **324**
  - GITPATH: **refs/heads/issues/**
- No projeto de publicação:
  - VERSAO: **324**

## Exemplo de branch na raiz do repositório
- Nome do branch: **S125.8-Alteração_AtosMonocráticos**
- No projeto de build, os campos devem ser preenchidos da seguinte forma:
  - VERSAO: **S125.8-Alteração_AtosMonocráticos**
  - GITPATH: **refs/heads/**
- No projeto de publicação:
  - VERSAO: **S125.8-Alteração_AtosMonocráticos**