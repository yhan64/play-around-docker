# After I went though this tutorial


# how to setup an app with redis with docker-compose
https://docs.docker.com/compose/gettingstarted/#step-3-define-services-in-a-compose-file
1. go through the tutorial on the above link
2. run `docker-compose up`
That's it.

NOTE:
1. `docker-compose` automatically links the redis with the app services accessing port '6379', which is the default exposed port of redis.
2. the redis container created through this process can NOT be accessed by other containers outside of services defined in `docker-compose`.
(docker: Error response from daemon: Cannot link to /playarounddocker_redis_1, as it does not belong to the default network)

# how to setup an app with redis without docker-compose
https://docs.docker.com/get-started/part2/#build-the-app
(start point is `app.py`)
1. `cd app`
2. run `docker build -t docker-init .`, which build an image based on `Dockerfile`, and `Dockerfile` uses `app.py` as an entry point
3. run `docker pull redis` to get redis image
4. run `docker run --name redis -p 6379:6379 redis` to create a container of reids. DO NOT forget to config the port!!!
5. run `docker run --name hello-redis-3 --link redis -p 4040:80 docker-init`, create a container of our app and link it to redis
(NOTE: you have to link the redis container here. Different containers may expose same port number, so define the redis port in app.py isn't sufficient)
6. open link `http://localhost:4040/` in browser

# how to remove all containers / images
## Delete all containers
docker rm $(docker ps -a -q)
## Delete all images
docker rmi $(docker images -q)
