
# how to setup an app with redis without docker-compose
https://docs.docker.com/get-started/part2/#build-the-app
(start point is `app.py`)
1. run `docker build -t docker-init .`, which build an image based on `Dockerfile`, and `Dockerfile` uses `app.py` as an entry point
2. run `docker pull redis` to get redis image
3. run `docker run --name redis -p 4001:6379 redis` to create a container of reids. DO NOT forget to config the port!!!
4. run `docker run -d --name hello-redis-3 --link redis -p 4040:80 docker-init`, create a container of our app and link it to redis
(NOTE: you have to link the redis container here. Different containers may expose same port number, so define the redis port in app.py isn't sufficient )
5. open link `http://localhost:4040/` in browser
