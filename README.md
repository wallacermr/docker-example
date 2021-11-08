# docker-example

Adicionando o arquivo docker-compose, e configurando o serviço do mysql;

Para rodar localmente, digitar os seguintes comandos:<br />
1. docker-compose up -d<br />
2. docker-compose exec db /bin/bash<br />
3. mysql -h localhost -uroot -p<senha_definida_MYSQL_ROOT_PASSWORD><br />
4. Na primeira vez que rodar dar permissão ao usuário definido <MYSQL_USER> GRANT ALL PRIVILEGES ON <banco_definido_MYSQL_DATABASE>.* TO '<MYSQL_USER>'@'%';<br />

No properties definir a config do banco local<br />
spring.datasource.url=jdbc:mysql://localhost:3306/<MYSQL_DATABASE><br />
spring.datasource.username=<MYSQL_USER><br />
spring.datasource.password=<MYSQL_PASSWORD><br />

importante: essas configs estão sendo feitas para o banco mysql, provavelmente para o postgres e outro banco, verificar as variaveis de config.

caso não utilize o docker-compose, segue o comando para executar a imagem:

docker run -d -p 3306:3306 --name mysql8 -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=<database_name> -e MYSQL_USER=<username> -e MYSQL_PASSWORD=<my_password>  mysql/mysql-server:8.0.16
  
docker exec -it mysql8 bash<br />
mysql -uroot -ppassword

GRANT ALL PRIVILEGES ON <banco_definido_MYSQL_DATABASE>.* TO '<MYSQL_USER>'@'%';

Caso não seja passado o usuario e o banco no comando docker é necessário cria-lo;

docker run -d -p 3306:3306 --name mysql8 -e MYSQL_ROOT_PASSWORD=password mysql/mysql-server:8.0.16;<br />
docker exec -it mysql8 bash<br />
mysql -uroot -ppassword<br />

CREATE DATABASE <databasename>;<br />
CREATE USER '<username>' IDENTIFIED BY '<user_password>';<br />
GRANT ALL PRIVILEGES ON <databasename>.* TO '<username>';<br />
