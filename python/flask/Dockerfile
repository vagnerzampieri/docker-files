FROM ubuntu

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN echo "deb http://archive.ubuntu.com/ubuntu/ $(lsb_release -sc) main universe" >> /etc/apt/sources.list

RUN apt-get update

RUN useradd -s /bin/bash -m app \
  && echo "app:app" | chpasswd \
  && echo "app ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN apt-get install -y tar git curl nano wget dialog net-tools build-essential

RUN apt-get install -y python python-dev python-distribute python-pip make libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev llvm libncurses5-dev

# Data Science
RUN apt-get install -y python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose

RUN pip install flask

USER app

ENV HOME /home/app

WORKDIR /home/app

RUN mkdir $HOME/Projects/

EXPOSE 80

CMD ['bash']
