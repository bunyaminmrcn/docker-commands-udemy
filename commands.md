# Udemy crash course

```sh

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
