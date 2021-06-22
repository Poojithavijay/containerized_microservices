# Containerized Microservice Mesh Development & Deployment using Python, Flask & Kubernetes

## Tasks Implemented

1. Build four simple microservices and wire them up in a Kubernetes cluster, e.g. using [Link](https://minikube.sigs.k8s.io/docs/start/).

2. The first microservice provides a simple web interface and allows the entry of a password. This password is sent to all the other microservices and the responses are displayed on this HTML page. 

3. The second microservice receives a password, calculates its strength and sends the score back to the caller. Please implement this from scratch. (See [Link](https://www.uic.edu/apps/strong-password/) for an example how to calculate the password strength.)

4. The third microservice receives a password, checks if the last 10 calls contained the same password and sends this information back to the caller.

5. The fourth microservice receives a password, checks if the password matches a password on a common password list on the Internet and sends this information back to the caller. (Simple text file with one password per line. Use [Link](https://pwlist.cfapps.eu10.hana.ondemand.com/passwords.txt)

6. Considered the following code qualities: object-oriented programming principles, clean code, design patterns, testing, documentation, etc. 


## Execution Instructions/Commands

1. *Optional* - Generate Self-Signed SSL Certificate for HTTPS:  
   > openssl req -x509 -newkey rsa:4096 -nodes -out cert.pem -keyout key.pem -days 365

2. Start minikube for the first time (only after wsl2, docker, minikube & kubectl are installed)
   > minikube start --driver=docker

3. Check Minikube Dashboard
   > minikube dashboard

4. Set minikube to use local docker daemon (Run this everytime a new shell session is started)
   > For Powershell: 'minikube docker-env | Invoke-Expression' \
   > For Unix: 'eval $(minikube docker-env)'

5. Build multiple Dockerfiles in the same project
   > docker build -f service_1.Dockerfile -t service_1:v1 . \
   > docker build -f service_2.Dockerfile -t service_2:v1 . \
   > docker build -f service_3.Dockerfile -t service_3:v1 . \
   > docker build -f service_4.Dockerfile -t service_4:v1 .

6. Deploy the images as pods in Kubernetes
   > kubectl create -f service-1.yml \
   > kubectl create -f service-2.yml \
   > kubectl create -f service-3.yml \
   > kubectl create -f service-4.yml

7. Check deployment status
   > kubectl get svc \
   > kubectl get deployments \
   > kubectl get pods

8. Start the services
   > minikube service --url --https service-1 \
   > minikube service --url --https service-2 \
   > minikube service --url --https service-3 \
   > minikube service --url --https service-4

9. *Optional* - Run the containers directly from the images built above (Without using Kubernetes)
   > docker run --name s_1 -itp 5000:5000 service:1 \
   > docker run --name s_2 -itp 5001:5001 service:2 \
   > docker run --name s_3 -itp 5002:5002 service:3 \
   > docker run --name s_4 -itp 5003:5003 service:4

10. Run the application by going to Chrome/Firefox browser & enter the URL displayed in the terminal (*Don't forget to use https*)

## Requirements

1. Python 3
2. flask
3. minikube
4. kubectl
5. hashlib
6. requests
7. pyopenssl (optional - to generate self-signed SSL certificate)


### Author

Poojitha Vijayanarasimha
