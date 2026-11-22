# docker

###### docker exec
```bash
docker exec -it rsyslog-x86-64 "/bin/bash"
```

###### docker ps
```bash
docker ps --no-trunc
```

###### Remove all containers including stopped containers
```bash
docker rm $(docker ps -a -q)
```

###### List docker images
```bash
docker image ls
```

###### List running docker containers
```bash
docker ps --no-trunc
```

###### List running docker containers
```bash
docker ps -a
```

###### Run a docker container in detached mode
```bash
docker run -d <image-name>
```

###### Run a docker container in interactive mode with a shell
```bash
docker run -it <image-name> /bin/bash
```

###### Shell into a running docker container
```bash
docker exec -it <container-name> /bin/bash
```

###### Apply a tag to an existing docker image
```bash
docker tag <existing-image> <hub-user>/<repo-name>[:<tag>]
```

###### Build a docker image from the `Dockerfile` in the current directory, with the given image name and the tag *latest*
```bash
docker build -t <image-name>:latest .
```

###### Build multiple docker images using docker-compose
```bash
docker-compose -f <docker-compose-file.yml> build --no-cache
```


###### Run multiple docker containers using docker-compose
```bash
docker-compose -f <docker-compose-file.yml> up
```

###### Run a docker container with a port mapping
```bash
docker run --name <container-name> -d -p <external-port>:<container-port> <image-name>:latest
```

###### Pull a docker image from the repositories
```bash
docker pull <image-name>:latest
```

###### Kill all containers including stopped containers
```bash
docker kill $(docker ps -a -q)
```

###### Remove all containers including stopped containers
```bash
docker rm -f $(docker ps -a -q)
```

###### Remove all docker images
```bash
docker image rm -f $(docker images -q)
```

####### System prune
```bash
docker system prune -a
```

###### Inspect a docker container
```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'
```

```bash
docker port <container>
```

```bash
docker network ls
```

```bash
docker network inspect <network-name>  
```

###### Commands I use to build verbecc-svc docker
```bash
cd verbecc-svc/python
docker build -t bretttolbert/verbecc-svc .
docker tag bretttolbert/verbecc-svc:latest bretttolbert/verbecc-svc:1.7.1
```

###### Configure aliases for git-bash windows environment
```bash
echo "alias python='winpty python.exe'" >> ~/.bashrc
echo "alias pytest='winpty pytest.exe'" >> ~/.bashrc
```

```bash
winpty docker exec -it verb_conjugate_fr_web //bin//sh
```

## docker --help
```

Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default "/home/brett/snap/docker/1458/.docker")
  -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST env var and default context set with "docker context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default "/home/brett/snap/docker/1458/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default "/home/brett/snap/docker/1458/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default "/home/brett/snap/docker/1458/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Management Commands:
  builder     Manage builds
  config      Manage Docker configs
  container   Manage containers
  context     Manage contexts
  image       Manage images
  manifest    Manage Docker image manifests and manifest lists
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

Run 'docker COMMAND --help' for more information on a command.

[1mTo get more help with docker, check out our guides at https://docs.docker.com/go/guides/[0m

```
