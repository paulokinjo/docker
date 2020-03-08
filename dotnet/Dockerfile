FROM ubuntu:18.04

LABEL maintainer="paulokinjo@hotmail.com"

ENV DOTNET_VERSION=2.1

RUN apt-get update \
    && apt install -y wget apt-transport-https \
    && wget -q https://packages.microsoft.com/config/ubuntu/19.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb \
    && dpkg -i packages-microsoft-prod.deb \
    && apt-get update \
                          # Install the .NET Core SDK
    && apt-get install -y dotnet-sdk-${DOTNET_VERSION} \        
                          # Install the ASP.NET Core runtime
                          aspnetcore-runtime-${DOTNET_VERSION}


