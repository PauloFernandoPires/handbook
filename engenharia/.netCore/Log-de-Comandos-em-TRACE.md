O .NET Core, por padrão, joga os comandos SQL que estão sendo executados no Trace Output da máquina. Porém, ele não mostra os parâmetros que foram utilizados no comando. Existe uma propriedade que pode ser definida na montagem do Contexto que permite mostrar essa informação que é o EnableSensitiveDataLogging().

Em nossos projetos, esse paramêtro só pode ser executado quando estivermos em ambiente de desenvolvimento. O trecho de código abaixo dá o exemplo.

```cs
        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            optionsBuilder.AddTcmrjAuditoriaInterceptor(httpContextAccessor);
            optionsBuilder.AddTcmrjDBLogInterceptor(logger);
            optionsBuilder.EnableDetailedErrors();
            if (environment.IsDevelopment())
            {
                optionsBuilder.EnableSensitiveDataLogging();
            }
        }
```

**OBS:** A propriedade **EnableDetailedErrors()** também deve ser habilitada em qualquer situação para facilitar o encontro do motivo do erro.

Com essa flag ativada, o Trace do Visual Studio passa a aparecer da seguinte forma.

```sql
Tcmrj.Atos.Web Information: 0 : 2022-05-30 12:05:38.221 -03:00 [Tcmrj.Atos.Web] [Information] Executed DbCommand ("1"ms) [Parameters=["@__appResourceId_0='601', @__appId_1='67'"], CommandType='Text', CommandTimeout='30']

SELECT [t].[AppId], [t].[Id], [t].[Description], [t].[ParentId], [t].[ResourceKey], [a0].[Id], [a0].[AppId], [a0].[CanDelete], [a0].[CanExecute], [a0].[CanInsert], [a0].[CanPrint], [a0].[CanSelect], [a0].[CanSpecial1], [a0].[CanSpecial2], [a0].[CanSpecial3], [a0].[CanUpdate], [a0].[GroupId], [a0].[ResourceId]
FROM (
    SELECT TOP(1) [a].[AppId], [a].[Id], [a].[Description], [a].[ParentId], [a].[ResourceKey]
    FROM [AppResources] AS [a]
    WHERE ([a].[Id] = @__appResourceId_0) AND ([a].[AppId] = @__appId_1)
) AS [t]
LEFT JOIN [Accesses] AS [a0] ON ([t].[AppId] = [a0].[ResourceId]) AND ([t].[Id] = [a0].[AppId])
ORDER BY [t].[AppId], [t].[Id], [a0].[Id]
```

Para ter acesso ao enviroment.IsDevelopment(), a criação do contexto precisa receber o IHostEnviroment como abaixo.

```cs
        private readonly IHostEnvironment environment;

        public AtosContext(IHostEnvironment environment)
        {
            this.environment = environment;
        }
```

