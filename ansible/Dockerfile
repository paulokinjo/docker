FROM ubuntu:18.04

LABEL maintainer="paulokinjo@hotmail.com"

RUN apt update \
    && apt install -y software-properties-common \
    && apt-add-repository --yes --update ppa:ansible/ansible \
    && apt install -y ansible 

CMD [""]