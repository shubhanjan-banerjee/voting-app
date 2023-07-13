# voting-app

kubectl create -f ./final-deployment/voting-app.deployment.yml
kubectl create -f ./final-deployment/result-app.deployment.yml
kubectl create -f ./final-deployment/worker-app.deployment.yml
kubectl create -f ./final-deployment/redis.deployment.yml
kubectl create -f ./final-deployment/postgres.deployment.yml
minikube service voting-app-service --url
minikube service result-app-service --url
