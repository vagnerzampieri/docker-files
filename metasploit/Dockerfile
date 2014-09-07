#
# Metasploit
# sudo docker build -t metasploit .
# sudo docker run --privileged -t -i metasploit /bin/bash
FROM ubuntu

MAINTAINER Vagner Zampieri <vgzampieri@gmail.com>

RUN apt-get -y update
RUN apt-get -y install build-essential zlib1g zlib1g-dev libxml2 libxml2-dev libxslt-dev locate libreadline6-dev libcurl4-openssl-dev git-core libssl-dev libyaml-dev openssl autoconf libtool ncurses-dev bison curl wget postgresql postgresql-contrib libpq-dev libapr1 libaprutil1 libsvn1 libpcap-dev sqlite3 libsqlite3-dev iptables
RUN apt-get -y install git-core postgresql curl ruby1.9.3 nmap gem

RUN gem install wirble sqlite3 bundler

RUN iptables -A INPUT -p tcp -dport 4444 -j ACCEPT

RUN cd /opt; git clone https://github.com/rapid7/metasploit-framework.git
RUN cd /opt/metasploit-framework; bundle install
CMD ./opt/metasploit-framework/msfconsole

EXPOSE 4444
EXPOSE 80
EXPOSE 8080
EXPOSE 22
