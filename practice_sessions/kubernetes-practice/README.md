# voting-app

brew install kubectl
brew install minikube

minikube start

kubectl cluster-info
minikube dashboard

kubectl get pods
kubectl get services
kubectl get replicasets
kubectl get deployments

kubectl get all

kubectl run msone-pod --image venuopalshatri/microserviceone:latest
kubectl get pods
minikube ssh
docker ps
exit

kubectl describe pod msone-pod  
kubectl delete pod msone-pod
// kubectl delete pod --all
kubectl get pods

kubectl run voting-app-pod --image shubhanjanweb/voting-app:latest
kubectl get pods
kubectl delete pods --all

kubectl create -f ./kubernetes-practice/voting-app/voting-app/voting-app.pod.yml
kubectl get pods
kubectl create -f ./kubernetes-practice/voting-app/voting-app/voting-app.service.yml
kubectl get svc
minikube ip
ping 192.168.49.2
kubectl describe pod voting-app-pod
ping 10.244.0.12

minikube service voting-app-service --url

kubectl delete pod --all
kubectl delete service --all

kubectl create -f ./kubernetes-practice/voting-app/result-app/result-app.pod.yml
kubectl get pods
kubectl create -f ./kubernetes-practice/voting-app/result-app/result-app.service.yml
kubectl get svc
minikube service result-app-service --url

kubectl create -f ./kubernetes-practice/voting-app/voting-app/voting-app.replicaset.yml
kubectl replace -f ./kubernetes-practice/voting-app/voting-app/voting-app.replicaset.yml

kubectl scale --replicas=6 replicaset voting-app-replicaset
kubectl delete replicaset voting-app-replicaset

kubectl create -f ./kubernetes-practice/voting-app/voting-app/voting-app.deployment.yml
kubectl get all
kubectl apply -f ./kubernetes-practice/voting-app/voting-app/voting-app.deployment.yml
kubectl describe deployment voting-app-deployment
kubectl rollout status deployment voting-app-deployment
kubectl rollout history deployment.apps/voting-app-deployment
kubectl describe deployment voting-app-deployment
kubectl rollout undo deployment.apps/voting-app-deployment

kubectl create -f ./kubernetes-practice/voting-app/voting-app/voting-app.deployment.yml
kubectl create -f ./kubernetes-practice/voting-app/result-app/result-app.deployment.yml
kubectl create -f ./kubernetes-practice/voting-app/worker-app/worker-app.deployment.yml
kubectl create -f ./kubernetes-practice/voting-app/redis/redis.deployment.yml
kubectl create -f ./kubernetes-practice/voting-app/postgres/postgres.deployment.yml

#examples

kubectl create deployment hello-minikube --image venuopalshatri/microserviceone:latest
kubectl expose deployment hello-minikube --type=NodePort - -port=3000
kubectl get services hello-minikube
minikube service hello-minikube
minikube service hello-minikube --url
kubectl get deployments
kubectl delete deployment --all
kubectl describe deployment <deploymentName>
kubectl rollout status <deploymentName>
kubectl rollout history <deploymentName> (observe revision number)
kubectl edit deployment deploymentname - -record (for update)

kubectl rollout undo <deployment Name>
kubectl create -f …..yml –record
kubectl get nodes
kubectl run <podeName> –image <imageName>
kubectl describe pod <podename>
kubectl get pods
kubectl delete pods - -all
kubectl get replicasets
kubectl describe replicaset <name of the replicaset>
kubectl scale replicaset <Name of the Replicaset> - -replica <NewValue>
kubectl edit replicaset <Name Of the replicaset>
