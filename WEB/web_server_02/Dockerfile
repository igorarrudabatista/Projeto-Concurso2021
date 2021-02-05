FROM nginx:1.12
RUN mkdir /usr/share/nginx/html/pag2/
COPY index.html /usr/share/nginx/html/pag2/

RUN apt-get clean
RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get install -y iputils-ping
RUN apt-get install -y net-tools


