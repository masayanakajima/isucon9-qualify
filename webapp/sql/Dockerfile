FROM mysql:5.7

WORKDIR /

EXPOSE 3306

RUN apt-get update
RUN apt-get install -y wget libdbd-mysql-perl libdbi-perl libio-socket-ssl-perl libnet-ssleay-perl libterm-readkey-perl
RUN wget https://www.percona.com/downloads/percona-toolkit/3.0.10/binary/debian/xenial/x86_64/percona-toolkit_3.0.10-1.xenial_amd64.deb
RUN dpkg -i percona-toolkit_3.0.10-1.xenial_amd64.deb