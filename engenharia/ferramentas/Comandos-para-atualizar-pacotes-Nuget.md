### Usar o Package Manager Console para visualizar quais pacotes do TCMRJ podem ser atualizados
```ps
get-package -update | where id -like Tcmrj* | select Id, projectName, Version | Format-Table -autosize -wrap
```

### Para atualizar de verdade
```ps
get-package -update | where id -like Tcmrj* | Update-Package
```