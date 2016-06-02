FROM ubuntu:14.04

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN useradd -s /bin/bash -m marvin \
  && echo "marvin:marvin" | chpasswd \
  && echo "marvin ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN \
  apt-key adv --keyserver keys.gnupg.net --recv-keys 09617FD37CC06B54 && \
  echo "deb http://dist.crystal-lang.org/apt crystal main" > /etc/apt/sources.list.d/crystal.list && \
  apt-get update && \
  apt-get install -y crystal gcc pkg-config libssl-dev git curl && \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER marvin

ENV HOME /home/marvin

RUN mkdir $HOME/Projects/

# Config bash
RUN curl -L https://gist.githubusercontent.com/vagnerzampieri/4492613/raw/0786fe30cd1235e74ac5da6599fdfb85396966c0/.bash_aliases -o ~/.bash_aliases
RUN curl -L https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh -o ~/.git-prompt.sh
RUN rm ~/.bashrc \
  && curl -L https://gist.githubusercontent.com/vagnerzampieri/cc926f7121e1d5efb4a7/raw/f6bba4ee4a1ef44d16858ac09abc57d3b636dfb5/.bashrc -o ~/.bashrc

WORKDIR $HOME/Projects

# App
EXPOSE 8080 8080
EXPOSE 3000 3000

CMD ["bash"]

