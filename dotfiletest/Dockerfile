# vim-tmux dotfile test
FROM     ubuntu
MAINTAINER Buddy Magsipoc

# make sure the package repository is up to date
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update

RUN apt-get install -y openssh-server
RUN apt-get install -y git

# Install tools
RUN apt-get install -y vim
RUN apt-get install -y tmux

# Clone dotfile and its submodules
RUN git clone --recursive http://github.com/keikun17/dotfiles /root/.dotfiles
RUN cd /root/.dotfiles && git submodule update --init --recursive

# Log folder
RUN mkdir /root/logs

USER root

# Prepare dotfiles
RUN ln -s /root/.dotfiles/vim /root/.vim
RUN ln -s /root/.dotfiles/vim/vimrc /root/.vimrc

# Install vim plugins
RUN vim  -c "source /root/.vimrc" +PluginInstall +qall > /root/logs/vim_plugininstall.log
# RUN vim +PluginInstall +qall > /root/logs/vim_plugininstall.log

RUN mkdir /var/run/sshd

# Copy ssh key so we can ssh into the server
RUN echo "IdentityFile ~/.ssh/id_rsa" >> /etc/ssh/ssh_config

RUN echo 'root:dotfiletest' |chpasswd

EXPOSE 22
CMD    /usr/sbin/sshd -D
