=======
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

## Prometheus + Node Exporter + Grafana
```bash
$ docker network create -d bridge monitoring-net

$ docker container run --rm -d --name node_exporter --hostname node_exporter --network monitoring-net -p 9100:9100 -p 26:22 paulokinjo/node_exporter

$ docker container run --rm -d --name prometheus --hostname prometheus --network monitoring-net -p 9090:9090 -p 27:22 paulokinjo/prometheus 

$ docker container run -d --rm -p 3000:3000 -p 28:22 --network monitoring-net --name grafana --hostname grafana paulokinjo/grafana
```

[1]: https://docs.docker.com/get-docker/
[2]: https://docs.docker.com/compose/install/
