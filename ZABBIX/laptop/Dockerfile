FROM ubuntu:20.04
RUN apt-get clean
RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get install -y iputils-ping
RUN apt-get install -y net-tools
RUN apt-get install -y iptables
RUN apt-get install -y vim
RUN apt-get install -y curl
RUN apt-get install -y zabbix-agent
RUN /etc/init.d/zabbix-agent restart 

ENTRYPOINT /bin/bash

