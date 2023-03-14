# Tabela de utilização de certificados

| certificado | descrição| servidores |
| ---|---|----|
| *.tcmnet.tc.br | Certificado Curinga | Certificate Store e IIS dos servidores TCM2016WEB1 <br> TCM2016WEB2 <br/> TCM2016ARR1 |
| pytcmweb.tcmnet.tcm | Para servidor Python de Produção |
| pytcmweb2.tcmnet.tcm | Para servidor Python de Homologação
| fwtcmrj | Firewall do TCMRio 
| tcmweb1p |  | [Certificate Store do TCMWEB1P e WinRM](engenharia/devops/Renovacao-de-Certificados#renovação-de-certificado-em-máquinas-no-iplan)
| tcmbdp |  | [Certificate Store do TCMBP e WinRM](engenharia/devops/Renovacao-de-Certificados#renovação-de-certificado-em-máquinas-no-iplan)
| tcmweb1s |  | [Certificate Store do TCMWEB1S, WinRM](engenharia/devops/Renovacao-de-Certificados#renovação-de-certificado-em-máquinas-no-iplan) e [RabbitMQ](engenharia/devops/Renovacao-de-Certificados-no-RabbitMQ)
| tcmweb2s |  | [Certificate Store do TCMWEB2S, WinRM](engenharia/devops/Renovacao-de-Certificados#renovação-de-certificado-em-máquinas-no-iplan) e [RabbitMQ](engenharia/devops/Renovacao-de-Certificados-no-RabbitMQ)
| tcmwebc |  | [Certificate Store do TCMWEBC e WinRM](engenharia/devops/Renovacao-de-Certificados#renovação-de-certificado-em-máquinas-no-iplan)
| tcmwebh |  | [Certificate Store do TCMWEBH e WinRM](engenharia/devops/Renovacao-de-Certificados#renovação-de-certificado-em-máquinas-no-iplan)
| svc-buildagent@tcmnet.tcm | Certificado usado para impersonar acesso a máquinas via WINRM | [Ver roteiro aqui](engenharia/devops/Renovacao-de-Certificados#renovação-de-certificado-do-svc-buildagent)
