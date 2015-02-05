FROM ubuntu:14.10

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get update

# Install dependencies
RUN apt-get install -qy software-properties-common \
  build-essential \
  dpkg \
  tmux \
  vim \
  curl \
  wget \
  unzip \
  git \
  libqt4-dev \
  libcurl4-openssl-dev \
  phantomjs \
  nodejs 

RUN useradd -s /bin/bash -m app \
  && echo "app:app" | chpasswd \
  && echo "app ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

USER app

ENV HOME /home/app

WORKDIR /home/app

# Install and Config RVM
ENV RVM_DIR $HOME/.rvm
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
RUN curl -L https://get.rvm.io | bash -s stable
RUN $RVM_DIR/scripts/rvm
RUN $RVM_DIR/bin/rvm install 2.1.5
RUN $RVM_DIR/bin/rvm alias create default ruby-2.1.5

RUN echo "gem: --no-ri --no-rdoc" > $HOME/.gemrc

# Config bash
RUN curl -L https://gist.githubusercontent.com/vagnerzampieri/4492613/raw/0786fe30cd1235e74ac5da6599fdfb85396966c0/.bash_aliases -o ~/.bash_aliases
RUN curl -L https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh -o ~/.git-prompt.sh
RUN rm ~/.bashrc \
  && curl -L https://gist.githubusercontent.com/vagnerzampieri/cc926f7121e1d5efb4a7/raw/f6bba4ee4a1ef44d16858ac09abc57d3b636dfb5/.bashrc -o ~/.bashrc

RUN mkdir $HOME/Projects/

# Install VIM
RUN git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim
RUN cd $HOME && git clone https://github.com/powerline/fonts.git \
  && cd $HOME/fonts/ && ./install.sh
RUN curl -L https://raw.githubusercontent.com/vagnerzampieri/vim-dot-files/master/ruby/.vimrc -o ~/.vimrc

# App
EXPOSE 8080 8080
EXPOSE 3000 3000

VOLUME $HOME/Projects

CMD ['bash']
