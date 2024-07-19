# Useful Commands

## Install Docker Compose
```bash
sudo apt install docker-compose
```

docker-compose.yml

```yaml
version: '3.8'

services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    depends_on:
      - db

  db:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: example
      MYSQL_DATABASE: mydatabase
      MYSQL_USER: user
      MYSQL_PASSWORD: password

```

Running Commands
Starting Services:
```bash
docker-compose up -d
```

Viewing Logs:
```bash
docker-compose logs
```

Viewing Logs for a Specific Service:
```bash
docker-compose logs web
```

Listing Containers:
```bash
docker-compose ps
```

Executing a Command in a Running Container:
```bash
docker-compose exec web sh
```

Stopping Services:
```bash
docker-compose stop
```

Removing Stopped Containers:
```bash
docker-compose rm
```

Restarting Services:
```bash
docker-compose restart
```

Scaling Services:
```bash
docker-compose up -d --scale web=3
```

Stopping and Removing All Resources:
```bash
docker-compose down
```

These commands will help you manage and troubleshoot your Docker Compose applications effectively.

## CLI Cheetsheet -> https://dockerlabs.collabnix.com/intermediate/docker-compose/#cli-cheatsheet 

### Example 
https://github.com/docker/awesome-compose/blob/master/elasticsearch-logstash-kibana/README.md
