# DockerAndRedis
Set up a Redis database management system using Docker, Set up a Redis replication database using Docker

# Commandline for demo redis on docker:

1. docker-compose up
2. docker ps
3. docker-compose exec redis-master bash
4. redis-cli
5. info
6. info replication

# Commandline for demo redis replication on docker:

# 1. network
docker network create redis

# 2. clustering

#redis-0

docker run -d --rm --name redis-0 `
    --net redis `
    -v ${PWD}/redis-0:/etc/redis/ `
    redis:6.0-alpine redis-server /etc/redis/redis.conf

#redis-1

docker run -d --rm --name redis-1 `
    --net redis `
    -v ${PWD}/redis-1:/etc/redis/ `
    redis:6.0-alpine redis-server /etc/redis/redis.conf


#redis-2

docker run -d --rm --name redis-2 `
    --net redis `
    -v ${PWD}/redis-2:/etc/redis/ `
    redis:6.0-alpine redis-server /etc/redis/redis.conf

## Test Replication

Technically written data should now be on the replicas

```
# go to one of the clients
docker exec -it redis-2 sh
redis-cli
auth "a-very-complex-password-here"
keys *

```
