Eventualmente, o Jenkins pede para atualizar o JRE que roda a aplicação. Isso deve ser atualizado da seguinte forma.

- Parar o serviço do Jenkins.
- Instalar o JRE desejado na máquina em que o Jenkins está hospedado.
- Ir até a pasta 'jre' do local onde o Jenkins está instalado e fazer um backup completo da pasta.
- Ir até a pasta do JRE que foi instalado na nova versão do java (ex: C:\Program Files\Java\jdk-11.0.15.1)
- Apagar todo o conteúdo da pasta 'jre' no Jenkins e copiar todo o conteúdo da pasta do novo Java instalado para lá.
- Ligar novamente o serviço do Jenkins.

