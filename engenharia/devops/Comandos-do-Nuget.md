O TCM tem um servidor do Nuget localizado em:
```console
\\unity\corp2\desenvolvimento\DESENVOL\NUGET
```

Na raiz da pasta existe o executável do Nuget que pode ser utilizado. A última versão colocada é a 6.1 (nuget_6.1)

## Como adicionar um pacote nuget no servidor interno
```console
\\unity\corp2\desenvolvimento\DESENVOL\NUGET\nuget_6.1.exe add <pacote.nupkg> -source \\unity\corp2\desenvolvimento\DESENVOL\NUGET
```

## Como adicionar vários pacotes de uma vez no servidor interno
- Colocar todos os pacotes em uma pasta única e executar
```
\\unity\corp2\desenvolvimento\DESENVOL\NUGET\nuget_6.1.exe init <diretório dos pacotes> -source \\unity\corp2\desenvolvimento\DESENVOL\NUGET
```

