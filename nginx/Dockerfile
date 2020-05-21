FROM ubuntu:18.04

LABEL maintainer="paulokinjo@hotmail.com"

# SO - Update and install packages
RUN apt-get update \
&&  apt-get install -y wget \
                       build-essential \
&&  apt-get clean

# SO SSH - 
RUN apt-get update -y && \
    apt-get install \
      vim \
      sshpass \
      net-tools \
      ssh \
      openssh-client \
      openssh-server \
      locales \
      iputils-ping -y 

# SO SSH -  remove some pointless services
RUN /usr/sbin/update-rc.d -f ondemand remove; \
  for f in \
    /etc/init/u*.conf \
    /etc/init/mounted-dev.conf \
    /etc/init/mounted-proc.conf \
    /etc/init/mounted-run.conf \
    /etc/init/mounted-tmp.conf \
    /etc/init/mounted-var.conf \
    /etc/init/hostname.conf \
    /etc/init/networking.conf \
    /etc/init/tty*.conf \
    /etc/init/plymouth*.conf \
    /etc/init/hwclock*.conf \
    /etc/init/module*.conf\
  ; do \
    dpkg-divert --local --rename --add "$f"; \
  done; \
  echo '# /lib/init/fstab: cleared out for bare-bones Docker' > /lib/init/fstab

RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

RUN ssh-keygen -t rsa -N "" -f ~/.ssh/id_rsa

RUN mkdir /var/run/sshd
RUN echo 'root:root' | chpasswd

# SO SSH -  SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

# NGINX
ARG NGINX_VERSION=1.17.10

ENV NGINX_BASE_URL=http://nginx.org
ENV NGINX_PACKAGE_NAME=nginx-${NGINX_VERSION}
ENV NGINX_EXTENSION=.tar.gz
ENV NGINX_DOWNLOAD_URL=${NGINX_BASE_URL}/download/${NGINX_PACKAGE_NAME}${NGINX_EXTENSION}

# NGINX - Donwload and extract
WORKDIR /tmp
RUN wget ${NGINX_DOWNLOAD_URL} \
&&  tar -zxvf ${NGINX_PACKAGE_NAME}${NGINX_EXTENSION}

# NGINX - Dependencies
RUN apt-get install -y libpcre3 \
                       libpcre3-dev \
                       zlib1g \
                       zlib1g-dev \
                       libssl-dev

# NGINX - config
WORKDIR /tmp/${NGINX_PACKAGE_NAME}
RUN ./configure \
    --sbin-path=/usr/bin/nginx \
    --conf-path=/etc/nginx/nginx.conf \
    --error-log-path=/var/log/nginx/error.log \
    --http-log-path=/var/log/nginx/access.log \
    --with-pcre \
    --pid-path=/var/run/nginx.pid \
    --with-http_ssl_module

# NGINX - Compile
RUN make \
&&  make install

# PORTS
EXPOSE 80 22

# COMMANDS
CMD /usr/bin/nginx \
&&  /usr/sbin/sshd -D