![Repo header](https://github.com/AleMorales9011/Entendendo-na-Pratica-a-Cultura-DevOps-com-Azure-DevOps/blob/120f2225812e22f00b136ec06b5b625668ad4daa/Repo%20header.jpg)
# 003-ARCHITECTURE-BFF PATTERN 
This project demonstrates how to use `Azure DevOps and Terraform` to implement the Backends for Frontends (BFF) pattern in Microsoft Azure. The BFF pattern is a software architecture pattern that allows you to create separate backend services for different front-end applications or interfaces. This approach helps **improve your applications' maintainability, scalability, and performance**. 

![Linux](https://img.shields.io/badge/Linux-000?style=for-the-badge&logo=linux&logoColor=FF00F6&color:FFF)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-000?style=for-the-badge&logo=postgresql&logoColor=FF00F6&color:FFF)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=FF00F6&color:FFF)

# Pre-requisites
>- An Azure subscription
>- An Azure DevOps organization
>- Terraform installed and configured

# Project Structure
This project is organized into the following directories:

>- **azure-pipelines:** This directory contains the Azure Pipelines YAML files that define the CI/CD pipeline for deploying the infrastructure and backend services.
>- **terraform:** This directory contains the Terraform configuration files that define the infrastructure resources in Azure.

# Problem
"Crafty Corner," a small online craft store, thrived with its website. But as they launched a mobile app, their **single backend became a bottleneck**. Balancing the needs of both platforms slowed development and frustrated teams.


>Demonstrating an API request to a backend service, which could be part of a BFF implementation:

![python code](https://github.com/AleMorales9011/Entendendo-na-Pratica-a-Cultura-DevOps-com-Azure-DevOps/blob/ad87f3320cc36d2140e2bf61e567f696dca749e0/python%20code.jpg)

# Old Architecture
![old architecture](https://github.com/AleMorales9011/Entendendo-na-Pratica-a-Cultura-DevOps-com-Azure-DevOps/blob/120f2225812e22f00b136ec06b5b625668ad4daa/old%20architechture.png)

# Solution
The **"Backends for Frontends"** approach saved the day. `Separate backends allowed independent optimization` for each platform, improving app speed and user experience. Sarah, the owner, could now focus on individual improvements, fostering efficient development and a happier team. In addition, a ***CI/CD pipeline** will be implemented in Azure DevOps to allow Sarah to create, modify, or eliminate infrastructure in the Azure Cloud from her local environment every time she commits a change **increasing its development team productivity by over 80%**.

>Creating cloud resources with Terraform


![terraform code](https://github.com/AleMorales9011/Entendendo-na-Pratica-a-Cultura-DevOps-com-Azure-DevOps/blob/a06788098dbdf544d83dc2a92eb1171325536c92/resource%20group%20with%20terraform.jpg)
# New Architecture
![new architecture](https://github.com/AleMorales9011/Entendendo-na-Pratica-a-Cultura-DevOps-com-Azure-DevOps/blob/120f2225812e22f00b136ec06b5b625668ad4daa/new%20architechture.png)

>Creating storage accounts in Azure with Terraform

![storage accounts with terraform](https://github.com/AleMorales9011/Entendendo-na-Pratica-a-Cultura-DevOps-com-Azure-DevOps/blob/bed83074fe1931c1ec6995a2af6149e34ae3a492/storage%20accounts%20witth%20terraform.jpg)

# Benefits of using the BFF pattern
>- **Improved maintainability:** By separating the backend into multiple services, you can change one service without affecting the others. This makes it easier to develop, test, and deploy changes.
>- **Increased scalability:** You can scale each backend service independently to meet the specific needs of the frontend application it serves.
>- **Enhanced performance:** By tailoring the backend services to the `specific requirements of each frontend`, you can improve the overall performance of your application. 

#  CI/CD Pipeline in Azure Dev Ops.
![Pipeline](https://github.com/AleMorales9011/Entendendo-na-Pratica-a-Cultura-DevOps-com-Azure-DevOps/blob/120f2225812e22f00b136ec06b5b625668ad4daa/Backend%20for%20Fronteds%20model.png)

>Initializing CI/CD pipeline with Terraform

![pipeline init](https://github.com/AleMorales9011/Entendendo-na-Pratica-a-Cultura-DevOps-com-Azure-DevOps/blob/0bda46320218fa3a2e28934cc13377a131ea86bd/Pipeline%20init.jpg)

# Benefits of CI/CD
>- **Faster software delivery:** CI/CD automates the build, test, and deployment process, significantly reducing the time it takes to deliver new features and bug fixes. This can lead to up to 100 times more frequent deployments.

>- **Improved software quality:** By automating testing within the pipeline, CI/CD `helps identify and fix bugs early` in the development process, leading to higher-quality software. This can result in a 30% to 90% reduction in defect escape rate.

>- **Increased collaboration and efficiency:** CI/CD pipelines `promote collaboration` by providing a central location for developers to track the progress of changes and identify potential issues early on. This streamlines the development process and reduces manual work, potentially leading to a 50% to 90% reduction in lead time for changes.

# Created Resources
![Resources](https://github.com/AleMorales9011/Entendendo-na-Pratica-a-Cultura-DevOps-com-Azure-DevOps/blob/120f2225812e22f00b136ec06b5b625668ad4daa/Resources%20created.jpg)

# Running Pipeline
![pipeline](https://github.com/AleMorales9011/Entendendo-na-Pratica-a-Cultura-DevOps-com-Azure-DevOps/blob/120f2225812e22f00b136ec06b5b625668ad4daa/Pipeline%20Success.jpg)





