DOCUMENTAÇÃO

Por: Igor de Arruda Batista
Janeiro /2021

LINK de Vídeo em execução:

https://vimeo.com/user102781272/review/505763557/9fd8866a73

INTRODUÇÃO:

1- Montar um ambiente utilizando o ​ Docker Compose​ , tendo como sistema operacional base
qualquer distribuição Linux, de modo a levantar um os seguintes servidores:
a) Firewall
b) Proxy Reverso
c) Web_Server_01
d) Web_Server_02
e) Zabbix

2- Realizar as configurações necessárias para que o ​ Laptop ​ acesse:
a) www.lab.local/pag1​ - página contida no Web_Server_01
b) www.lab.local/pag​ 2 - página contida no Web_Server_02
Considere o seguinte:
a) O Web_Server_01 deverá exibir uma página com o número do CPF.
b) O Web_Server_02 deverá exibir uma página com o e-mail.

3- Ativar o monitoramento dos serviços e dispositivos contidos no diagrama acima no Zabbix.
--



####################

CRIANDO AS VLAN:

####################

### VLAN 10

  docker network create -d macvlan \
  --subnet=192.168.1.0/24 \
  --gateway=192.168.1.1 \
  -o parent=enp3s0.10 \
  vlan10

---

### VLAN 20
  
  docker network create -d macvlan \
  --subnet=192.168.2.0/24 \
  --gateway=192.168.2.1 \
  -o parent=enp3s0.20 \
  vlan20
  
 
-----

### VLAN 30
  
      docker network create -d macvlan \
  --subnet=10.1.1.0/24 \
  --gateway=10.1.1.1 \
  -o parent=enp3s0.30 \
  vlan30

##################

Servidores WEB

##################

Estrutura das pastas WEB:

Proxy-reverso
├── default.conf
├── docker-compose.yml
└── Dockerfile

web_server_01
├── docker-compose.yml
├── Dockerfile
└── index.html

web_server_02
├── docker-compose.yml
├── Dockerfile
└── index.html


Passo 1:
Acesse o diretório /WEB/proxy-reverso e digite:
docker-compose build
docker-compose up -d
Este comando irá construir o container com as configurações/informações necessárias dentro do arquivo Dockerfile

Passo2:
# Dentro do diretório /WEB/web_server_01
Digitar o comando:
docker-compose build
docker-compose up -d
Este comando irá construir o container com as configurações/informações necessárias dentro do arquivo Dockerfile

Passo3:
Dentro do diretório /WEB/web_server_02
# Digite os comando:
docker-compose build
docker-compose up -d
# Este comando irá construir o container com as configurações/informações necessárias dentro do arquivo Dockerfile

#Verique os 3 container com o comando:
 docker ps 
 
 
 
##################
 
 ZABBIX:
 
################## 


Estrutura de Pasta Zabbix:

└── docker-compose.yml


Passo 1
execute o comando a baixo:
docker-compose build
docker-compose up -d
* Este comando irá construir o container Zabbix

Não consegui inserir as informações dos containers dentro do arquivo Dockerfile para que a aplicação do Zabbix subisse com as configurações de monitoramento já configuradas. Portanto os passos a baixo é para a inclusão dos Containers/Hosts de forma manual.

Passo2
Acesse a aplicação para iniciar o cadastro dos hosts:
localhost:8081/zabbix 
Usuário: Admin
Senha: zabbix

Passo 3  
- Logado na aplicação zabbix, acesse Configuração > Hosts > Criar Host
- Digite o nome do Host
- Insira-o no Grupo correspondente (no nosso caso Linux Servers)
- Insira o IP do servidor que deseja monitorar em:
  Interfaces do agente.
- Na aba Templates, adicione os serviços que deseja monitorar. (Em nosso caso vamos adicionar os serviços de HTTP Nginx e ICMP)
- Faça o mesmo cadastro para os demais containers que deseja monitorar.

################### 
OBS. Para descobrir os IPs dos seus containers digite o comando a baixo:
execute o comando a baixo para descobrir os IPs dos seus container criados anteriormente.

docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' Nome do seu container

Exemplo:

docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' zabbix web_server_01 web_server_02 proxy-reverso laptop firewall

###################


############

FIREWALL

###########

Estrutura da pasta Firewall

FIREWALL
├── docker-compose.yml
└── Dockerfile

Passo 1. 
Execute os comandos abaixo para a criação da imagem Firewall.

docker-compose build
docker-compose up -d



#####


 
