É possível visualizar qual será o modelo gerado pelo EF depois de que todas as configurações foram setadas pelo Fluent API e o OnModelCreating.

Isso pode ajudar bastante na hora de identificar um erro que esteja acontecendo durante a montagem do modelo.

É só colocar uma linha a mais no repositório que será utilizado para pegar a informação. Lembrar de depois apagar antes de commit.

```cs
public class AcompanhamentoRepository : EfRepository<Acompanhamento, AtosContext>, IAcompanhamentoRepository
{
    public AcompanhamentoRepository(AtosContext atosContext) : base(atosContext)
    {
        var x = atosContext.Model.ToDebugString(MetadataDebugStringOptions.LongDefault);
    }
}
```


Fontes: 
  - https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.entitytypeextensions.todebugstring?view=efcore-5.0
  - https://www.meziantou.net/entity-framework-core-view-the-model-as-text.htm


