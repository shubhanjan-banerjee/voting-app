# voting-app

docker pull redis
docker pull postgres

docker run -d --name redis redis
docker run -d --name db -e POSTGRES_HOST_AUTH_METHOD=trust postgres
// docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres

docker build -t shubhanjanweb/voting-app ./vote
docker build -t shubhanjanweb/result-app ./result
docker build -t shubhanjanweb/worker-app ./worker
docker run -d --name=vote -p 3001:80 shubhanjanweb/voting-app
docker run -d --name=result -p 3002:80 shubhanjanweb/result-app
docker run -d --name=worker shubhanjanweb/worker-app

docker stop 8 6 2 f 9
docker rm 8 6 2 f 9
// docker rm $(docker ps -a)

docker run -d --name redis redis
docker run -d -e POSTGRES_HOST_AUTH_METHOD=trust --name db postgres
docker run -d --name vote --link redis:redis -p 3001:80 shubhanjanweb/voting-app
docker run -d --name result --link db:db -p 3002:80 shubhanjanweb/result-app
docker run -d --name worker --link db:db --link redis:redis shubhanjanweb/worker-app

docker push shubhanjanweb/voting-app
docker push shubhanjanweb/result-app
docker push shubhanjanweb/worker-app

#docker compose
