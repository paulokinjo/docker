FROM ubuntu:18.04

LABEL maintainer="paulokinjo@hotmail.com"

RUN apt update \
    && apt install -y software-properties-common \
                      unzip \
                      python-pip \
    && apt-add-repository --yes --update ppa:ansible/ansible \
    && apt install -y ansible \
    && pip install setuptools

RUN apt install -y wget && wget https://bootstrap.pypa.io/get-pip.py \
    && python get-pip.py

RUN apt-get install -y sshpass

COPY ./ansible.cfg ~/ansible.cfg
CMD [""]