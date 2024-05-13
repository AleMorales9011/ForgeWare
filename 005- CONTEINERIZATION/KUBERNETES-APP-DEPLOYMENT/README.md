## Kubernetes App Deployment
This project demonstrates the deployment of a multi-tier application on Kubernetes, a container orchestration platform. The application consists of a MySQL database and a PHP backend service.

## Methodology
Conteinerized Application deployment using Dockers and Kubernetes to illlustrate containerization best practices. All the required services for propper functioning of the application were created from scratch.

## Results
The provided YAML defines several Kubernetes resources for deploying a MySQL database and a PHP application:

```ruby
# Persistent Volume Claim to request persistent storage to kubernetes
apiVersion: v1 
kind: PersistentVolumeClaim
metadata:
  name: mysql-datos
spec:
  accessModes:
  - ReadWriteOnce # Read write acces for one pod at a time
  resources:
    requests:
      storage: 10Gi # Request 10 Gb of storage
  storageClassName: standard-rwo # Pre configured sorage class that proviions Read write once volumes

---

# Mysql deployment
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
spec:
  selector:   # Select pods with the label "mysql"
    matchLabels:
      app: mysql
  template: # a blueprint for creating pods
    metadata: # Data about the data
      labels:  # Identify pods 
        app: mysql
    spec:
      containers:
      - image: alemorales9011935/projeto-database:1.0 # Docker image used for the deployment
        args:
        - "--ignore-db-dir=lost+found"  # Ignores previous deployments
        imagePullPolicy: Always # Ensure the image is pulled even if exists locally
        name: mysql
        ports:
        - containerPort: 3306
          name: mysql
          
        volumeMounts:
        - name: mysql-dados
          mountPath: /var/lib/mysql/ # where the containers will be storaged
      volumes:
      - name: mysql-dados
        persistentVolumeClaim:
          claimName: mysql-dados

---

apiVersion: apps/v1
kind: Deployment
metadata:
  name: php
  labels:
    app: php
spec:
  replicas: 6 # Amounts of pods to be created
  selector:
    matchLabels:
      app: php
  template:
    metadata:
      labels:
        app: php
    spec:
      containers:
      - name: php
        image: alemorales9011935/projeto-backend:1.0
        imagePullPolicy: Always # Always pulls the image from the registry even if it exists locally.
        ports:
        - containerPort: 80
```

The configuration below defines a php-Service. This configuration creates a ```LoadBalancer``` service for your PHP application. Kubernetes will work with your cloud provider to set up an external load balancer that will distribute traffic across multiple pods running the PHP application. The external IP address for accessing the service will be dynamically assigned by the cloud provider and can be retrieved later using ```kubectl get service php```.

```ruby
apiVersion: v1 
kind: Service # Defines the type of kubernetes object
metadata:
  name: php
spec:
  selector: # This service will find and route traffic to pods that have the label app: php. 
    app: php  # Select pods with the label "app: php"
  ports:
  - port: 80 # The port users will acces from outside the cluster
    targetPort: 80 # The port php application listens 
  type: LoadBalancer # Type of Service

```
The configuration below creates a ClusterIP service for a MySQL database. A ClusterIP service is only accessible from within the Kubernetes cluster. Pods within the cluster can access the MySQL service at mysql-connection on port ```3306```. 

```ruby
---
apiVersion: v1
kind: Service
metadata:
  name: mysql-connection
spec:
  ports:
  - port: 3306
  selector: 
    app: mysql
  clusterIp: None

```
## Deployment Script
The provided script is a Bash script for deploying the project.

```ruby

#!/bin/bash

echo "Creating images..."

docker build -t alemorales9011935/projeto-backend:1.0 backend/.
docker build -t alemorales9011935/projeto-database:1.0 database/.

echo "Pushing images..."

docker push alemorales9011935/projeto-backend:1.0
docker push alemorales9011935/projeto-database:1.0

echo "Creating Services..."

kubectl apply -f ./services.yml --validate=false

echo "Criating Deployment"

kubectl apply -f ./deployment.yml --validate=false

```





