# DockerAndRedis
Set up a Redis database management system using Docker, Set up a Redis replication database using Docker

Commandline for demo redis on docker:

docker-compose up
docker ps
docker-compose exec redis-master bash
redis-cli
info
info replication

Commandline for demo redis replication on docker:

# remember to update above in configs!

docker network create redis
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
