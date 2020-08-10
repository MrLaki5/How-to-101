## Usefull docker instructions:
* Docker containers itself are set of process isolation rules done through namespacing and control groups on linux os. Docker on windows and osx has linux VM in background. They have specific filesystem and start commands that are aquired from docker images.



### Viewing:
* View all images:
``` bash
docker images
```

* View running containers:
``` bash
docker ps [-a]
# -a is to see all containers, even ones that are stopped.
```



### Starting:
* Run docker compose and create containers
``` bash
docker-compose -f <path to docker compose file> up [-d] 
# -d is used for deattached mode
```

* Run container (create and start) from clean image with terminal attached to it:
``` bash
docker run -it <image name> /bin/bash
# -i: used to connect out terminal with standard input of linux process in wich out container is run
# -t: format text that is going (i/o)
```

* Start stopped container
``` bash
docker start [-a] <container id>
# -a: attached mode, to see logs of container
```



### Interacting with running containers:
* Run one command inside container:
``` bash
docker exec <container name> <command>
```

* Attach to container and run commands:
``` bash
docker exec -it <container name> bash
# -i: used to connect out terminal with standard input of linux process in wich out container is run
# -t: format text that is going (i/o)
exit
```

* See docker container logs:
``` bash
docker logs [-f] <container name>
# -f is for attached mode
```



### Stopping:
* Stop running container:
``` bash
docker stop <container name>
```

* Killing running container without extra time for stopping:
``` bash
docker kill <container name>
```

* Stop all running containers:
``` bash
docker stop $(docker ps)
```

* Stop running containers from specific docker compose file:
``` bash
docker-compose -f <path to docker compose> stop
```



### Removing:
* Remove all containers and images:
``` bash
docker system prune
```

* Remove stopped container:
``` bash
docker rm <container name>
```

* Remove all containers that are stopped:
``` bash
docker rm $(docker ps -aq)
```

* Remove docker image that is not used by any container:
``` bash
docker rmi <container image name>

# Remove all untagged images:
docker rmi $(docker images -f "dangling=true" -q)
```

* Remove all docker images that are not used by any containers:
``` bash
docker rmi $(docker images)
```



### Docker machine:
* See all machines:
``` bash
docker-machine ls
```

* Attach to running machine:
``` bash
# First step is not needed
docker-machine env <machine name>
eval "$(docker-machine env <machine name>)"
```

* Start stopped machine:
``` bash
docker-machine start <machine name>
```

* Stop running machine:
``` bash
docker-machine stop <machine name>
```

* Create new virtualbox docker machine:
 ``` bash
# Note: virutalbox must be installed.
docker-machine create --driver virtualbox <machine name>
```

* Create new machine on local device that is running docker:
``` bash
docker-machine create --driver generic --generic-ip-address <device ip address> --generic-ssh-user <username on device> --generic-ssh-key <path to ssh key> --engine-storage-driver overlay2 <machine name>
```



### Building image:
* Building image from dockerfile:
``` bash
docker build -t <image name (see convention below)> <path to dockerfile>
# Name convention when building custom images: <Docker id>/<Project name>:<version>
```

* Building image from container:
``` bash
# Make sure private key is added to ssh-agent and that publick key is copied to targeted device.
docker commit -c <default command> <Running container ID>
# Default command will be done when container is started from image we are creating. eg: 'CMD ["echo Hello world!"]'
```




### Docker file construction:
* Copy command with from argument can be used in case where two separate dockerfile images are used merged in one new (where one is used in FROM and other in this COPY).
``` bash
COPY --from=<name|index> <src> <dest>
# name: name of docker image from dockerhub
# index: release number of docker image
# src: content that will be copied from given image (for whole image use /)
# dest: place where content will be copied in new docker container
# Note: if case where two images are being merged is used, it's best to make sure two images have same origin and to use src: / and dest /
```
