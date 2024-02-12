# gitlab

## mac

### docker

Set enviroment

```
echo "export GITLAB_HOME=~/_garage/gitlab" >> ~/.zshrc

source .zshrc
```

Pull gitlab image

```
docker pull zengxs/gitlab:16.8-ce
```

Start gitlab container

```
docker run --detach --publish 8443:443 --publish 8080:80 --publish 2222:22 --name gitlab --volume $GITLAB_HOME/config:/etc/gitlab --volume $GITLAB_HOME/logs:/var/log/gitlab --volume $GITLAB_HOME/data:/var/opt/gitlab --shm-size 256m zengxs/gitlab:16.8-ce
```

root パスワード表示

```
sudo docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```

### docker-compose

Create docker-compose.yml

```
version: '3.6'
services:
  gitlab:
    image: 'zengxs/gitlab:16.8-ce'
    restart: always
    hostname: 'localhost'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://localhost'
        # Add any other gitlab.rb configuration here, each on its own line
    ports:
      - '8080:80'
      - '8443:443'
      - '2222:22'
    volumes:
      - '$GITLAB_HOME/config:/etc/gitlab'
      - '$GITLAB_HOME/logs:/var/log/gitlab'
      - '$GITLAB_HOME/data:/var/opt/gitlab'
    shm_size: '256m'
```

Start gitlab container

```
docker-compose up -d
```

# Reference

[zengxs/gitlab](https://hub.docker.com/r/zengxs/gitlab/tags)

[Mac mini で始める「GitLab」入門！](https://www.ai-lab.app/722/)

[GitLab Docker イメージ](https://gitlab-docs.creationline.com/ee/install/docker.html#install-gitlab-using-docker-compose)
