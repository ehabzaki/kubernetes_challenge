# kubernetes_challenge


I followed this blog post to dockerize a ruby on rails app using Docker compose
blog link:
https://semaphoreci.com/community/tutorials/dockerizing-a-ruby-on-rails-application

github repo for docker tutorial:
https://github.com/ehabzaki/instabug-challenge

I want to Do it, but with using kubernetes

In order to prep for the Kubernetes deploy ,I packaged the Rails Docker image and push to a Docker registry(DockerHub).
DockerHub repo link 
https://hub.docker.com/r/ehab123/drkiq/
now,I need to translate the docker-compose.yml config into Kubernetes resources.
This is a repo of translation
https://github.com/ehabzaki/kubernetes_challenge


1- create the secret to store postgres password
 kubectl create secret generic postgres-pass --from-literal=password=yourpassword

 
2- create the Kube resources for postgres
 
kubectl create -f drkiq-postgres-persistentvolumeclaim.yaml
 
kubectl create -f postgres-service.yaml

kubectl create -f postgres-deployment.yaml


3-create the kube resources for redis

kubectl create -f drkiq-redis-persistentvolumeclaim.yaml

kubectl create -f redis-service.yaml

kubectl create -f redis-deployment.yaml


4-create the kube resources for sidekiq

kubectl create -f sidekiq-service.yaml

kubectl create -f sidekiq-deployment.yaml


5-Kube Job

kubectl create -f job_migration.yaml


6-create app resources

kubectl create -f drkiq-service.yaml
kubectl create -f drkiq-deployment.yaml

7-created  Ingress resource
kubectl create -f ingress.yaml

8- check status of pods

kubectl get pods -w  




