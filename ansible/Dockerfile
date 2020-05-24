FROM paulokinjo/ssh

LABEL maintainer="paulokinjo@hotmail.com"

RUN apt-get update \
    && apt-get install -y software-properties-common \
    unzip \
    python-pip \
    wget \
    && apt-add-repository --yes --update ppa:ansible/ansible \
    && apt-get install -y ansible \
    && pip install setuptools \ 
    && pip install pywinrm==0.2.2

RUN wget https://bootstrap.pypa.io/get-pip.py \
    && python get-pip.py 

# default command
CMD ["supervisord", "-c", "/etc/supervisor.conf"]
