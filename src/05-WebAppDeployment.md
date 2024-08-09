![banner](images/9.jpg)

# Deploying a web application with Kubernetes

60 minutes

This project demonstrates the deployment of a `multi-tier application` on Kubernetes, a container orchestration platform. The application consists of a MySQL database and a PHP backend service.

# Methodology

Containerized Application deployment using `Dockers and Kubernetes` to illustrate containerization best practices. All the required services for the proper functioning of the application were created from scratch.

# Table Of Content

- Persistent Volme Claim
- MySQL Database Deployment
- PHP Deployment
- Load Balancer Service
- MySQL Database Service
- Deployment Script
- Conclusion

# Persistent Volme Claim

The provided YAML snippet is a well-structured Persistent Volume Claim (PVC) requesting persistent storage in Kubernetes. 

This PVC effectively requests `10 Gigabytes` of persistent storage with `ReadWriteOnce` access for a single Pod at a time. The `standard-two` StorageClass dictates where and how this storage will be provisioned.

```ruby
# Persistent Volume Claim to request persistent storage to Kubernetes
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

```

# MySQL Database Deployment

This deployment creates pods running a `MySQL container` with persistent storage for the database data. The provided code snippet defines a deployment for a `MySQL` database container in Kubernetes.

```ruby
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

```

# PHP Deployment

The provided YAML defines a `Kubernetes deployment` configuration for a PHP application. This YAML describes a deployment that creates six pods running the container image alemorales9011935/projeto-backend:1.0. These pods will be labeled with `app: php` and will expose their application on `port 80`.

```ruby
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

# Load Balancer Service

The configuration below defines a `php-Service`. This configuration creates a ```LoadBalancer``` service for your PHP application. 

Kubernetes will work with your cloud provider to set up an `external load balancer` that will distribute traffic across multiple pods running the PHP application. 

The external IP address for accessing the service will be dynamically assigned by the cloud provider and can be retrieved later using `kubectl get service php`.

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

# MySQL Database Service

The configuration below creates a `ClusterIP Service` for a MySQL database. A ClusterIP service is only accessible from within the Kubernetes cluster. Pods within the cluster can access the MySQL service at mysql-connection on port `3306`.

```ruby
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

### Deployment Script

The provided script is a Bash script for deploying the project.

```ruby

#!/bin/bash

echo "Creating images..."

docker build -t alemorales9011935/projeto-backend:1.0 backend/.  # Build docker image.
Creates a self-contained executable package for running an application
docker build -t alemorales9011935/projeto-database:1.0 database/. 

echo "Pushing images..."

docker push alemorales9011935/projeto-backend:1.0 # Uploading a completed Docker image to a Docker registry.
docker push alemorales9011935/projeto-database:1.0

echo "Creating Services..."

kubectl apply -f ./services.yml --validate=false # Figure out how to achieve
the desired state of the infrastucture we define.

echo "Criating Deployment"

kubectl apply -f ./deployment.yml --validate=false # Controls the validation behaviour.

```

# Conclussion

This repository serves as a `solid foundation` for Kubernetes deployment. 
