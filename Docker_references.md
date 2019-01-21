


## Docker basic commands:

- docker info —>info about how many containers,images e.t.c
- docker <mngmt commands><sub-commands><options> —>docker command format , older way is - -docker <command><options> ((both works)
- docker container run --publish 80:80 --detach nginx —> to start container in background
- docker container ls. —> list of containers(use -a to list all containers)
- docker container stop {container_id} -> to stop a container
- docker container logs {containerName} to see the logs
- docker container top {container Name) —> list the processes running in docker container
- docker container rm -f(to forcibly remove a container even if it is running)
- docker container inspect — details and configuration of a container
- docker container stats — live performance statistics of a container
- docker container update --help —> Update configuration of one or more containers even if they are running

## Docker shell commands:

- docker container run -it —> start new container interactively
- docker container run exec -it —> run additional commands inside container (exec runs only inside a cotainer which is already started)
- docker container run --rm -it --name ununtu ubuntu:14.04 bash(to run bash command at the time of container creation, exec works only on already running/stopped containers)
- docker container run -it --name nginx nginx bash -> to run bash shell without SSH
- docker container start -ai {containerName} —> to start container in shell mode if it is stopped
- docker container exec -it {containerId} bash—>Run a command in a running container —> when we exit from this shell, container wont stop bcz exec will start additional process and it wont effect existing one

## Docker Networking:

- docker container port {container} —> to get the port number on which we are mapping the traffic
- docker container inspect --format '{{ .NetworkSettings.IPAddress }}' {conainerId} —> to get IP address of a container
- docker network ls - to get the list of N/W’s
- docker network inspect {networkName} —> we can see images in this command output id they r mapped
- docker network create {networkName} —> to create a network, which will create with default driver bridge, we can use —driver to specify the driver, otherwise default option it will take(bridge)
- docker container run -p 81:80 --name nginx2 --network {networkName} -d nginx (to create with specific network}
- docker network connect {netwrokId} {containerId}, use disconnect in place of connect to disconnect from a network

## Docker networkd:DNS

- docker exec -it {containerName} ping {anotherContainer}— using this we can ping another a container from other container(prerequistie: they both should be in same network) using built in DNS network
- docker container run --network-alias search --net test -d elasticsearch:2 —> to create a container with DNS alias(—network-alias) and with network test
- docker container run --rm --net test alpine nslookup search —> it will search for nslookup DNS entry “search” inside that n/w
- If we run “docker container run --rm --net test centos curl -s search:9200” it will give different different outputs between two DNS servers

## Docker Images:

- docker image history {image_name} —> will list the changes in a image..not changes in container, whatver we do a change on a image it will create a new layer
- docker image inspect nginx —> returns the metadata of that image
- docker image tag mongo (new name ex:deekshith:mango} —> to tag an existing image with different name
- cat ~/.docker/config.json —this file will have all the credentials(In Mac it will store in keychain)
- docker image push {imageName} —> to push to docker hub after login using “docker login” command

## DockerFIle:

- docker image build -t customnginx .

## Docker Volumes:

- docker volume prune —> to cleanup unused volumes
- docker image inspect mysql
- docker volume ls —> will list the volumes
- docker volume inspect {volumeName} —> will give info about that volume
- docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True -v mysql-db:/var/lib/mysql mysql(named volume)
- docker volume create —> required to do this before “docker run” to use custom drivers and labels

## Bind Mount:

- docker container run -d --name nginx -p 80:80 -v $(pwd):/usr/share/nginx/html nginx —> mounting a directory

## Docker Compose:

- docker-compose up —> to start (use docker-compose -d to start the service in background)
- docker-compose down —> to stop
- docker-compose logs —> to see the logs
- docker-compose top -> to see the list of processes
- docker-compose down -v —> to remove named volumes
- docker-compose down —rmi —> Iyt will remove the image at the time of removing compose

## Docker Swarm:

- “docker info” command output, we can see whether Swarm is acive or not. By default it will be inactive.
- docker swarm init —> to initilize docker swarm
- docker node ls —> it will give the node(manager) which got created
- docker service —help(service in swarm replaces docker run)
- docker service create alpine(image) ping 8.8.8.8 —> to create a service with alpine image and we are using ping in that one to just check the service
- docker service ls —> to list the services
- docker service ps {service_name} —> to get more o/p
- docker service update {serviceName} --replicas 3 —> to run 3 replicas
- docker service update --help(it will have more options compared to docker container update --help)..using this we can do more things like scaling containers and changing conf etc.
- docker service rm {serviceName}—> It will also deletes the containers which r started through this service

## Swarm with 3 nodes:

- docker-machine(using https://labs.play-with-docker.com/p/bd25oqe08n7000d50rl0#bd25oqe0_bd25p4gabk8g008i6k8g)
- use “docker swarm init --advertise-addr 192.168.-63” to initlize the swarm where —advertise-ipaddr is the one which is accebile ,ABove command O/P will have the command for joining swarm, copy that and paste it in other nodes to join them,We cant run docker swarm command in the sub nodes, we need to run from manager to promote nodes
- docker node update --role manager node2 —> to update node2 as a manager an see docker node ls
- Use “docker swarm join-token manager” to get the manager token and paste that in node command to add as a manager
- docker service create --replicas 3 alpine ping 8.8.8.8 —> to create with 3 replicas
- Now try docker service ls or node ls or service ps

## Overlay Multi-Host networking example:

Run below commands in 3 node cluster in play-with-docker.com

- add “—driver overlay” at the end of “docker network create” to create a swarm wired bridge network where containers across hosts on same virtual networkwill communicate each other
- docker service create --name postgres --network mydrupal -e POSTGRES_PASSWORD=mypass postgres(to create a service with custom
- docker service create --name drupal -p 80:80 --network mydrupal drupal, After running these commands you can access the application in all the nodes

## swarm-app-1 assignment:
- docker service create --name vote --replicas 2 -p 80:80 --network frontend

## Docker stack:

- docker stack deploy -c example-voting-app-stack.yml voteapp where “example-voting-app-stack.yml” is yaml file and voteapp is name of the stack, use the same command if you make any changes to the yml file, it will take new ones
- check docker stack —help for more options

## Swarm Secrets:

- docker secret create psql_user psql_user.txt —> to create a new secret “psql_user”, you should have a file with name psql_user.txt already
- echo "myDBpAssWORD" | docker secret create psql_pass - -> second way, here we are passing via CLI using “-“ at last
- docker secret ls , docker secret inspect
- docker service create --name psql --secret psql_user --secret psql_pass -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_pass -e POSTGRES_USER_FILE=/run/secrets/psql_user postgres, It will map the values of the secret files into the env variables. Now we can see the secrets data inside the container in “/run/secrets/“ directory. Refer the documentation of this postgres official image for env variables
- docker service update --secret-rm. —> to remove the secret
- docker stack deploy -c docker-compose.yml mydb —> for stack

## Full App Lifecycle With Compose:
- docker-compose up -d
- docker-compose -f docker-compose.yml -f docker-compose.test.yml up where “docker-compose.yml” is default file, “docker-compose.test.yml” is override file for CI env, it will recreate the containers with the new compose file eventhough containers are running with the command in 1st point
- use docker inspect {containerName} to see the config
- docker-compose -f docker-compose.yml -f docker-compose.prod.yml config —> this will generate a config file which will have the combined config of default and prod compose file
Docker service update:
- docker service create -p 8088:80 --name web nginx:1.13.7 It will create a service with one node
- docker service scale web=5 —> to increae the replicas, similar to update command, docker service scale allows you to change the number of replicas for more than one service, compared to docker service update --replicas which allows you to change only one service at a time.
- docker service update --image nginx:1.13.6 web to update image, it will roll the update one replica at a time
- docker service update —pub;ish-rm 8088 —publish-add 9090:80
- docker service update --publish-rm 8088 --publish-add 9090:80 web
- docker service update --force web —> like restarting even though there are no changes, so that if there is increase in nodes, the load will get distributed equally

## Docker healthcheck:

- docker container run --name p2 -d --health-cmd="pg_isreay -U postgres || exit 1" postgres:9.6 where “pg_isreay -U postgres || exit 1” is the healthcheck command for postgres and now we can see healthcech in status in docker container ls comand, it will be in default starting stage for 30 sec. We can see this healthcheck in docker inspect command
- docker service create --name postgres2 --health-cmd="pg_isready -U postgres || exit 0" postgres , it will be in starting stage for 30 sec, then only it will go to running state

## Docker System:

- docker system df —> will tell you the space used by images,container,local volumes
- docker system prune —> will remove all the things except the running container and its volumes.
- docker image prune, docker container prune …we can use this also
- docker system prune -a —>Remove all unused images not just dangling ones
- “export DOCKER_STACK_ORCHESTRATOR='swarm' “to switch orchestrator from Kubernetees to swarm mode

