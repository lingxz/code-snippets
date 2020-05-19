# Introduction

List all containers \(running and exited\)

```bash
docker ps -a
```

Build an image with a dockerfile in the current directory

```text
docker build -t image_name:tag_name .
```

Run a docker container

```text
docker run image_name:tag_name
```

```text
docker run -d --name container_name -p 80:80 -p 443:443 --net network_name -v /path/of/file/in/host:/path/of/file/in/container image_name:tag_name
```

* `-d` detached mode
* `--name` specify the name you want to call this container
* `-p` ports mapping
* `--net` network to put it on
* `-v` volumes to mount

Start and go into interactive mode of last created container

```text
docker start -a -i `docker ps -q -l`
```

* `docker start` start a container \(requires name or ID\)
* `-a` attach to container
* `-i` interactive mode
* `docker ps` List containers
* `-q` list only container IDs
* `-l` list only last created container

Start and go into interactive mode of a specific container

```text
docker exec -it container_name_or_id /bin/bash
```

Remove dangling images

```text
docker rmi $(docker images -qa -f 'dangling=true')
```

