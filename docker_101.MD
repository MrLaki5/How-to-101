## Usefull docker instructions:



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

* Run container from clean image with terminal attached to it:
``` bash
docker run -ti <image name> /bin/bash
```



### Interacting with running containers:
* Run one command inside container:
``` bash
docker exec <container name> <command>
```

* Attach to container and run commands:
``` bash
docker exec -it <container name> bash
# To leave attached container use:
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

* Stop all running containers:
``` bash
docker stop $(docker ps)
```

* Stop running containers from specific docker compose file:
``` bash
docker-compose -f <path to docker compose> stop
```



### Removing:
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