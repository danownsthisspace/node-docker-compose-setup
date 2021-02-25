This is an example of an basic docker setup for a node api

### Build image:

    docker build -t node-api:v1 .

## create network

    docker network create node-api-network

## Start MYSQL:
    
    docker run \
    --rm \
    -d \
    --name mysql_server \
    -e MYSQL_DATABASE='test_db' \
    -e MYSQL_USER='dan' \
    -e MYSQL_PASSWORD='secret' \
    -e MYSQL_ROOT_PASSWORD='secret' \
    --network node-api-network \
    mysql:8.0 

    
## Start node-api

    docker run \
    --rm \
    --name node-app \
    --network node-api-network \
    -p 3000:3000 \
    -v $(pwd):/app \
    node-api:v1 

## Stop running container using

    docker stop node-app
    docker stop mysql_server

## or start using

    docker-compose up

## and stop using

    docker-compose down
    