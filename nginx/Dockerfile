FROM paulokinjo/ssh

LABEL maintainer="paulokinjo@hotmail.com"

# SO - Update and install packages
RUN apt-get update \
  &&  apt-get install -y wget \
  build-essential \
  &&  apt-get clean

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
EXPOSE 80

# default command
WORKDIR /tmp
COPY ./supervisor.conf .
RUN cat ./supervisor.conf >> /etc/supervisor.conf
CMD ["supervisord", "-c", "/etc/supervisor.conf"]
