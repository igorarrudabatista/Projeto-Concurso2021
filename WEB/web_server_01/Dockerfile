FROM nginx:1.12
RUN mkdir /usr/share/nginx/html/pag1/
COPY index.html /usr/share/nginx/html/pag1/

RUN apt-get clean
RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get install -y iputils-ping
RUN apt-get install -y net-tools
RUN apt-get install -y vim
RUN apt-get install -y curl
RUN apt-get install -y zabbix-agent
RUN /etc/init.d/zabbix-agent restart
