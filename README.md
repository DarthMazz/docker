# docker

## nginx

docker image get
```
docker pull nginx
```
docker container run
```
docker container run --name testnginx -d -p 8080:80 nginx
```

## nodejs

### reference

https://nodejs.org/ja/docs/guides/nodejs-docker-webapp/

docker image get
```
docker pull nginx:16
```
docker container run
```
docker container run --name testnodejs -it node:16 /bin/bash
```
docker build
```
docker build . -t yo4taka/node-web-app
```
docker container run
```
docker container run -p 49160:8080 -d yo4taka/node-web-app
```
docker attach
```
docker exec -it <container id> /bin/bash
```
docker detach
```
exit
```

## docker-compose
```
docker-compose up --build
```
