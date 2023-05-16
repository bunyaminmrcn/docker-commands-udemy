# Udemy crash course



```sh

# Print Working Directory
pwd
> /home/can/Desktop/workspace/docker/udemy-tuts
```

```sh

### video.70 ###


### video.71 ###

## Raft Consensus algoritm

### video.72 ###
docker swarm init --advertise-addr 192.168.0.13
docker info

docker swarm join-token manager # to add a manager will output a string like
> docker swarm join --token SWMTKN-1...     192.168.0.13:2377

docker swarm join-token worker
> docker swarm join --token SWMTKN-1...     192.168.0.13:2377


docker node ls # shows all nodes
> ID    HOSTNAME    STATUS      AVAILABILITY    MANAGER STATUS
>       node1       Ready       Active          Leader #leader
>       node2       Ready       Active          Reachable # manager but passive
>       node3       Ready       Active          Reachable # manager but passive
>       node4       Ready       Active          
>       node5       Ready       Active          

docker service create --name test --replicas=5 -p 8080:80 nginx
docker service ps test
> ID    NAME        IMAGE           NODE         DESIRED STATE
>       test.1      nginx:latest    node1        Running
>       test.2      nginx:latest    node2        Running
>       test.3      nginx:latest    node3        Running 
>       test.4      nginx:latest    node4        Running    
>       test.5      nginx:latest    node5        Running




### video.73 ###
### video.74 ###

docker service create --help
docker service create --name test nginx
docker service ls
>ID     NAME    MODE            REPLICAS    IMAGE
>xhk    test    replicated      1/1         nginx

docker service inspect test
docker service logs test

docker service scale test=3 # scale the service

docker service rm test # remove tthe service

docker service create --name glb --mode=global nginx # create global container

### video.75 ###

### video.76 ###
docker network create -d overlay over-net

docker service create --name web  --network over-net -p 8080:80  --replicas=3 ozgurozturknet/web

docker service create --name db  --network over-net ozgurozturknet/fakedb


### video.77 ###

docker node ls
docker network create -d overlay over-net
docker service create --name websrv --network over-net -p 8080:80 --replicas=10 ozgurozturknet/web:v1
docker service ls

docker service ps websrv

docker service update --help

# update service
docker service update --detach --update-delay 5s --update-parallelism 2 --image ozgurozturknet/web:v2 websrv

docker service rollback --detach websrv


### video.78 ###

# activate swarm mode
docker swarm init

###
`username.txt`
matrax
`sifre.txt`
P@ssw4rd1
### 

# create a secret
docker secret create username ./username.txt
docker secret create pass ./sifre.txt

docker secret ls

docker secret inspect pass
echo 'This is a test' | docker secret create test -

docker service create -d --name secret_test --secret username --secret pass --secret test ozgurozturknet/web



###
docker exec -it 9f7a sh

cd /run && cd secrets
ls
> username pass test
cat pass
> P@ssw4rd1

###


echo "asdfghjkl" | docker secret create pass2 -

# Update the secret
docker service update --secret-rm pass --secret-add pass2  secret_test



### video.79 ###

[docker-compose.yml](https://github.com/ozgurozturknet/AdanZyeDocker/blob/master/kisim6/bolum79/docker-compose.yml)
[video](https://www.udemy.com/course/adan-zye-docker/learn/lecture/19809756#overview)
# Change sections


# docker-stack

docker stack deploy -c ./docker-compose.yml firststack
docker stack ls
docker stack services firststack
> ID    NAME                MODE        REPLICAS
> gun   firststack_websrv   replicated  3/3
> mwd   firststack_mysqldb  replicated  1/1

docker service ps firststack_websrv

docker stack rm firststack

```
