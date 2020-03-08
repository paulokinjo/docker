FROM paulokinjo/pk-dotnet-core:latest

LABEL maintainer="paulokinjo@hotmail.com"

# Add the Mono repository to your system
RUN apt install -y apt-transport-https dirmngr \
    && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
    && echo "deb https://download.mono-project.com/repo/ubuntu vs-bionic main" | tee /etc/apt/sources.list.d/mono-official-vs.list \
    && apt update

# Install MonoDevelop
RUN apt-get install -y monodevelop

#  Installing MonoGame
RUN wget http://www.monogame.net/releases/v3.6/monogame-sdk.run \
    && chmod +x monogame-sdk.run \
    && ./monogame-sdk.run

# Add Monogame Template
RUN dotnet new --install MonoGame.Template.CSharp

WORKDIR /home

CMD [""]
