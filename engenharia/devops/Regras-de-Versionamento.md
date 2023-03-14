- O código de versionamento segue influência deste [documento](https://semver.org/lang/pt-BR/).
- A versão terá 3 números separados por ponto chamados de versão Maior (*MAJOR*), versão Menor (*MINOR*) e Versão de Correção (*PATCH*) (maior.menor.correção).
- Cada número pode ter no máximo 3 algarismos pois existem limitações em script do Jenkins e de publicação de scripts de banco. Então, a maior versão possível é 999.999.999.
- Sempre que seja necessário criar uma nova versão, a seguinte regra deve ser seguida:
1. É a primeira tag do Sprint no repositório?
    1. A primeira tag será <Número do Sprint>.1.1
2. É uma tag para marcar o lançamento inicial em produção do Sprint?
    1. Ou seja, o Sprint ainda não tinha nada lançado em produção.
    2. Seguir o padrão <Número do Sprint>.<Incrementar Versão Menor>.1
    3. Criar um branch dentro do repositório com o nome **releases/<Número do Sprint>.<Versão Menor Definida>.x**
3. É uma tag para para marcar correção em branch de release existente? (normalmente é uma correção de bug em produção)
    1. Pelo nome do branch de release, usar a mesma versão Maior e Menor e incrementar somente a versão de Correção.
4. É uma tag que não tem relação branch de release? (Normalmente são usadas para gerar pacotes nuget em ambiente de desenvolvimento.)
    1. Confirmar qual versão está publicada em produção executando o seguinte [script](http://git/asi/Geral/-/blob/master/Ferramentas/VersaoDeSistemasPublicados.ps1).
    2. A versão Maior do que está publicado em produção é igual a versão Maior atual do desenvolvimento?
        1. Caso Não:
            1. Verificar qual é a última versão cadastrada e incrementar a versão de Correção
        2. Caso Sim:
            1. Verificar se a última versão Menor cadastrada é uma versão publicada em produção. 
            2. Caso a última versão Menor não seja do branch de release, usar a mesma versão Menor e incrementar a versão de Correção.
            3. Caso a última versão Menor seja do branch de release, incrementar a versão Menor e colocar 1 na versão de Correção.
        

Exemplos seguindo ordem cronológica:
- Primeira tag de novo Sprint 122:
  - Tag 122.1.1 (regra 1.1)
- Commit e necessidade de criação de pacote Nuget 
  - Tag 122.1.2 (regra 4.2.1.1)
- Novo Commit e necessidade de criação outro pacote Nuget
  - Tag 122.1.3 (regra 4.2.1.1)
- Desenvolvimento completado e publicação em produção
  - Tag 122.2.1 (regra 2.2) (OBS: pode ser em cima do mesmo commit do 122.1.3)
  - Criação de branch 'releases/122.2.x' (regra 2.3)
- Erro em produção corrigido
  - Tag 122.2.2 (regra 3.1)
- Novo commit no master com necessidade de criação pacote Nuget
  - Tag 122.3.1 (regra 4.2.2.3)
- Novo Erro em produção corrigido e commit no branch 'releases/122.2.x'
  - Tag 122.2.3 (regra 3.1)
- Novo commit no master com necessidade de criação de pacote Nuget
  - Tag 122.3.2 (regra 4.2.2.2)

Acabou o Sprint 122 e começou o Sprint 123
- Primeira tag de novo Sprint 123:
  - Tag 123.1.1 (regra 1.1)
- Commit e necessidade de criação de pacote Nuget 
  - Tag 123.1.2 (regra 4.2.1.1)
- Erro em produção corrigido
  - Tag 122.2.4 (regra 3.1)
- Desenvolvimento completado e publicação em produção
  - Tag 123.2.1 (regra 2.2) (OBS: pode ser em cima do mesmo commit do 123.1.2)
  - Criação de branch 'releases/123.2.x' (regra 2.3)