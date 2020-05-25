FROM ubuntu:18.04

LABEL maintainer="paulokinjo@hotmail.com"

ENV TERRAFORM_VERSION=0.12.23

RUN apt update \
    && apt install -y unzip \ 
                      wget \
    && wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
    && unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
    && mv terraform /usr/local/bin/ 

CMD [ "" ]
