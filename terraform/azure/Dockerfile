FROM paulokinjo/pk-terraform

LABEL maintainer="paulokinjo@hotmail.com"

RUN apt-get install -y ca-certificates \
                       curl \
                       apt-transport-https \
                       lsb-release \
                       gnupg
        
RUN curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null

RUN AZ_REPO=$(lsb_release -cs) \
    && echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | tee /etc/apt/sources.list.d/azure-cli.list

RUN apt-get update \
    && apt-get install -y azure-cli

RUN wget https://aka.ms/downloadazcopy-v10-linux \
    && tar -xvf downloadazcopy-v10-linux \
    && rm -f /usr/bin/azcopy \
    && cp ./azcopy_linux_amd64_*/azcopy /usr/bin/ \
    && apt install -y gnome-keyring \
                      keyutils