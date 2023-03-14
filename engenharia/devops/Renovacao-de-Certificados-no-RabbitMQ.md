- Pegar no user manager o certificado (.pfx) que será usado para o TLS do site administrativo do RabbitMQ

  - Máquinas internas do TCM usarão o certificado *.tcmnet.tcm
  - Máquinas externas (IPLAN) usarão o certificado de cada uma. Exemplo: TCMWEB1S usará o certificado tcmweb1s, assim por diante.

- No final das contas, são necessários 3 arquivos:
### 1. O arquivo público do certificado raiz (formato BASE64)
- Ir na própria máquina local do desenvolvedor e abrir o certmgr.msc, localizar o certificado raiz do etcm e exportá-lo no formato base64. 

### 2. O arquivo público do certificado do servidor (formato BASE64)
-	Baixar do UserManager o certificado correspondente da máquina (ex: _.tcmnet.tcm.pfx ou tcmweb1s.pfx)
-	Jogar o certificado numa pasta temp da máquina local
-	Rodar o seguinte comando para gerar o arquivo público

```
"C:\Program Files\Git\usr\bin\openssl" pkcs12 -clcerts -nokeys -in "C:\temp\<NOME DO ARQUIVO>.pfx" -out "C:\temp\<NOME DO ARQUIVO>.crt" -password pass:<SENHA DO CERTIFICADO> -passin pass:<SENHA DO CERTIFICADO>
```

### 3. O arquivo da chave privada do certificado do servidor
- Rodar o seguinte comando para extrair a chave privada.
```
"C:\Program Files\Git\usr\bin\openssl" pkcs12 -nocerts -in "C:\temp\<NOME DO ARQUIVO>.pfx"  -out "C:\temp\<NOME DO ARQUIVO>.key" -password pass:<SENHA DO CERTIFICADO> -passin pass:<SENHA DO CERTIFICADO> -passout pass:<SENHA DO CERTIFICADO>
```
- Rodar o seguinte comando para remover a chave privada do gerado acima
```
"C:\Program Files\Git\usr\bin\openssl" rsa -in "C:\temp\<NOME DO ARQUIVO>.key" -out "C:\temp\<NOME DO ARQUIVO>.key" -passin pass:<SENHA DO CERTIFICADO>
```

- Os arquivos devem ser colocados na pasta **\Users\<USUÁRIO QUE INSTALOU O RABBITMQ>\AppData\Roaming\RabbitMQ**
- O serviço do RabbitMQ precisa ser reiniciado para considerar o novo certificado.
  - No caso de cluster, realizar o restart um de cada vez e esperar voltar o anterior a sincronizar com o que estava em pé.