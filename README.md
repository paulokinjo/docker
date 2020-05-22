# Docker

### Before you Start

1. Install docker

## Planning

```bash
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh
$ sudo usermod -aG docker $USER
$ docker info
```

## Running docker compose

```bash
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$ sudo chmod +x /usr/local/bin/docker-compose
$ docker-compose --version
```

[1]: https://docs.docker.com/get-docker/
[2]: https://docs.docker.com/compose/install/
