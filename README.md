### Repository for the K8s in 1 hour video

#### K8s manifest files 
* mongo-config.yaml
* mongo-secret.yaml
* mongo.yaml
* webapp.yaml

#### K8s commands

##### start Minikube and check status
    minikube start --vm-driver=hyperkit 
    minikube status

##### get minikube node's ip address
    minikube ip

##### get basic info about k8s components
    kubectl get node
    kubectl get pod
    kubectl get svc
    kubectl get all

##### get extended info about components
    kubectl get pod -o wide
    kubectl get node -o wide

##### get detailed info about a specific component
    kubectl describe svc {svc-name}
    kubectl describe pod {pod-name}

##### get application logs
    kubectl logs {pod-name}
    
##### stop your Minikube cluster
    minikube stop

<br />

> :warning: **Known issue - Minikube IP not accessible** 

If you can't access the NodePort service webapp with `MinikubeIP:NodePort`, execute the following command:
    
    minikube service webapp-service

<br />

#### Links
* mongodb image on Docker Hub: https://hub.docker.com/_/mongo
* webapp image on Docker Hub: https://hub.docker.com/repository/docker/nanajanashia/k8s-demo-app
* k8s official documentation: https://kubernetes.io/docs/home/
* webapp code repo: https://gitlab.com/nanuchi/developing-with-docker/-/tree/feature/k8s-in-hour


<br />

#### DEMO commands

Installation
* Docker installed and running
* Install Minikube & follow steps from Minikube site (kubectl gets installed as dependency)
* minikube start --driver docker
* minikube status

Prerequisite Images
1. docker pull mongo:5.0
2. docker pull sachinvashist/nextjs-docker:latest
	
Cluster Setup
* git clone https://github.com/ErSachinVashist/k8-config-files.git
* cd k8-config-files
* kubectl apply -f mongo-config.yaml
* kubectl apply -f mongo-secret.yaml
* kubectl apply -f mongo.yaml
* kubectl apply -f webapp.yaml
* kubectl get all

Expose Service
* minikube service $SERVICE_NAME

K8 Cluster UI Dashboard
* kubectl apply -f kubernetes-dashboard.yaml
* kubectl apply -f service-account.yaml
* kubectl -n kubernetes-dashboard create token admin-user
* kubectl proxy
* Open http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

