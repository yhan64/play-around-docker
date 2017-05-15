# After I went though this tutorial 
https://docs.docker.com/get-started/part2/#build-the-app

# how to setup an app using redis based on docker without docker-compose
(start point is `app.py`)
1. run `docker build -t docker-init .`, which build an image based on `Dockerfile`, and `Dockerfile` uses `app.py` as an entry point
2. run `docker pull redis` to get redis image
3. run `docker run --name redis -p 6379:6379 redis` to create a container of reids. DO NOT forget to config the port!!!
4. run `docker run --name hello-redis-3 --link redis -p 4040:80 docker-init`, create a container of our app and link it to redis
5. open link `http://localhost:4040/` in browser

# how to remove all containers / images
## Delete all containers
docker rm $(docker ps -a -q)
## Delete all images
docker rmi $(docker images -q)
