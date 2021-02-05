FROM nginx:1.12

COPY default.conf /etc/nginx/conf.d/default.conf


RUN apt-get clean
RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get install -y iputils-ping
RUN apt-get install -y net-tools
