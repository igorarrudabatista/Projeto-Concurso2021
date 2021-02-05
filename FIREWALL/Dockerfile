FROM ubuntu:16.04
RUN apt-get clean
RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get install -y iputils-ping
RUN apt-get install -y net-tools
RUN apt-get install -y iptables
RUN apt-get install -y vim
RUN apt-get install -y curl
RUN apt-get install -y zabbix-agent

RUN iptables -A FORWARD -s 192.168.1.0/24 -d 10.1.1.0/24 -j ACCEPT
RUN iptables -A FORWARD -d 192.168.1.0/24 -s 10.1.1.0/24 -j ACCEPT
RUN iptables -A FORWARD -s 10.1.1.0/24 -d 192.168.1.0/24 -j ACCEPT
RUN iptables -A FORWARD -d 10.1.1.0/24 -s 192.168.1.0/24 -j ACCEPT  
ENTRYPOINT /bin/bash
