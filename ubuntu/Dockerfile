FROM ubuntu:18.04

LABEL maintainer="paulokinjo@hotmail.com"

# Installs openssh-server
RUN apt update \
    && apt install -y openssh-server \
    wget \
    curl \
    vim \
    git

# Install packages
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install pwgen supervisor
RUN mkdir -p /var/run/sshd && sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config && sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config && sed -i "s/PermitRootLogin.*/PermitRootLogin yes/g" /etc/ssh/sshd_config

ADD set_root_pw.sh /set_root_pw.sh
ADD run.sh /run.sh
RUN chmod +x /*.sh

ENV AUTHORIZED_KEYS **None**

RUN mkdir -p /var/log/supervisor

# Add the supervisor configuration file
ADD ./supervisord.conf /etc/supervisor/supervisord.conf

EXPOSE 22
CMD ["/run.sh"]