- Pode ser que seja necessário desabilitar o Recaptcha no Portal do Jurisdicionado
- Esse controle pode ser desabilitado automaticamente em tabela no banco PORTAL_ETCM.
- O sistema trocará a validação do Recaptcha por um componente .NET mais antigo.

```sql
USE PORTAL_ETCM

UPDATE app.DbSettings
SET [Value] = 'false'
WHERE SettingKey = 'ReCaptcha_Ativado'
```