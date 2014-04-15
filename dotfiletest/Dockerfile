# vim-tmux dotfile test
FROM     ubuntu
MAINTAINER Buddy Magsipoc

# make sure the package repository is up to date
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update

RUN apt-get install -y openssh-server
RUN apt-get install -y git

RUN apt-get install -y vim
RUN apt-get install -y tmux

RUN git clone http://github.com/keikun17/dotfiles /root/.dotfiles

RUN mkdir /var/run/sshd

# Copy ssh key so we can ssh into the server
RUN echo "IdentityFile ~/.ssh/id_rsa" >> /etc/ssh/ssh_config

RUN echo 'root:dotfiletest' |chpasswd

EXPOSE 22
CMD    /usr/sbin/sshd -D
