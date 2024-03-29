# aws
<br/>

## EC2 (Iaas)

* *(cria uma máquina pura apenas com Sistema Operacional)*

* Criar a conta na AWS https://console.aws.amazon.com

* Criar o alarme de custos no Cloudwatch https://console.aws.amazon.com/cloudwatch/home?region=us-east-1

* Criar a primeira instância EC2 -> Launch Instance -> Ubuntu Server

* Acessar a máquina e criar a chave SSH (selecionar a instância e clicar em "Connect")
	* `sudo ssh -i springbootdemo.pem ubuntu@ec2-52-87-238-210.compute-1.amazonaws.com`

* Instalar a JRE: 
	* `sudo apt-get update && apt-get install openjdk-8-jre`

* Instalar o Tomcat:
	* `sudo apt-get install tomcat8`

* Iniciar o Tomcat:
	* `sudo service tomcat8 start

* Liberar o firewall(acesso externo), copiar o Public DNS:
	* `ec2-52-87-238-210.compute-1.amazonaws.com`

* Testar o Tomcat, no navegador colocar o DNS:
	* `ec2-52-87-238-210.compute-1.amazonaws.com`

* Instalar o Mysql server:
	* `sudo apt-get mysql-server`

* Conectar no Mysql:
	* `mysql`
	* `create database nomedabase;`
	* `show databases;`

* Alterar a senha do root no Mysql:
	* `FLUSH PRIVILEGES;`
	* `ALTER USER 'root'@'localhost' IDENTIFIED BY '1234';`

* Deploy da aplicação:
	* copiar o arquivo da app para dentro da máquina:
		* `sudo scp -i springbootdemo.pem loja.war ubuntu@ec2-52-87-238-210.compute-1.amazonaws.com:~`
	* conectar na máquina:
		* `sudo ssh -i springbootdemo.pem ubuntu@ec2-52-87-238-210.compute-1.amazonaws.com`
	* copiar o arquivo loja.war pra dentro do Tomcat:
		* `sudo mv loja.war /var/lib/tomcat8/webapps/`
	* varificar o log do Tomcat:
		* `sudo cat /var/lib/tomcat8/logs/localhost.2019-12-01.log`
	* setar a senha do mysql no tomcat, criando uma variável de ambiente:
		* `cd /usr/share/tomcat8/bin`
		* `sudo nano setenv.sh`
		* `export senha=1234`
	* reiniciar o Tomcat
		* `sudo service tomcat8 stop`
		* `sudo service tomcat8 start

## Escalabilidade vertical
* Isso significa melhorar o CPU, HD ou a memória RAM
* AWS EC2: basta parar a instancia e mudar o tipo da instância (Menu Instance Settings -> Change Instance Type)

## Escalabilidade horizontal
* usar uma segunda maquina para rodar a aplicação.

## Escalar o banco e Configurar o Amazon RDS
* selecionar a opção RDS https://console.aws.amazon.com/rds/home?region=us-east-1#
* RDS: provê um banco de dados relacional totalmente pronto.
* conectar e testar o banco command line: 
	* `mysql -u root -pMinhaSenha -h mysql-catalogo.cfs9hbfn73y.us-east-1.rds.amazonaws.com`
* 

