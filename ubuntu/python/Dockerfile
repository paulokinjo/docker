FROM paulokinjo/pk-ubuntu

LABEL maintainer="paulokinjo@hotmail.com"

RUN apt install -y software-properties-common \
    && add-apt-repository ppa:deadsnakes/ppa -y \
    && apt install -y python3.7 \
                      python3-openpyxl
