# Docker LogAnalyzer
Docker webapp [Adiscon LogAnalyzer](https://loganalyzer.adiscon.com/)
* Version: 4.1.12

* Based/Forked from https://github.com/vsc55/docker-loganalyzer

## Create Container:
```bash
docker create --name LogAnalyzer --restart always -p 80:80/tcp -v /doker/data:/data edino/docker-loganalyzer:arm64
docker container start LogAnalyzer
```

## Run Container:
```bash
docker run -d --restart always -p 80:80/tcp -v /doker/data:/data edino/docker-loganalyzer:arm64
```

## Docker Compose:

```bash
version: '3.8'

services:
  LogAnalyzer:
    image: edino/docker-loganalyzer:arm64
    container_name: LogAnalyzer
    restart: always
    ports:
      - "80:80"
    volumes:
      - /docker/data:/data
    networks:
      my_network:
        ipv4_address: 192.168.1.2  # Replace with your desired container IP
    healthcheck:
      test: ["CMD", "/health_check.sh"]
      interval: 4m
      timeout: 10s
      retries: 3
    logging:
      driver: json-file
      options:
        max-size: "10m"
        max-file: "3"
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
      restart_policy:
        condition: any

networks:
  my_network:
```


# Links:
Docker Hub: https://hub.docker.com/r/edino/docker-loganalyzer
