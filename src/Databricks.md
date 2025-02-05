# Azure Databricks: Overview

60 minutes - DevOps - Data Engineering

# Introduction
In the realm of big data, machine learning algorithms require pre-processed data to perform calculations and generate meaningful results. Take, for example, a product or video recommendation algorithm. For it to function effectively, it must store and process vast amounts of user interaction data, such as viewed, saved, and liked products. This data is then compared in real-time with similar data from other users. By applying probabilistic algorithms, the system identifies common patterns and ultimately delivers personalized product recommendations to the user.

# Table of Contents
1. Data Pipelines
2. Apache Spark
3. Data Bricks
4. Main Use Cases
5. Components
6. Apache Spark vs Data Bricks
7. Data Bricks: ETL Data Pipeline(overview)
8. Data Bricks: CI-CD 

# Data Pipelines
A data pipeline is a series of processes that automate the movement and transformation of data from one system to another, ensuring that raw data is efficiently converted into actionable insights.

# Apache Spark
Apache Spark is the Databricks precesor, an open-source, distributed computing system that provides fast, in-memory data processing capabilities for big data workloads, supporting tasks like batch processing, machine learning, and stream analytics.

# Data Bricks
Databricks is a managed, cloud-based platform built on Apache Spark that simplifies Spark's deployment, scaling, and collaboration, offering additional features like auto-scaling, integrated notebooks, and seamless integration with cloud services, while Apache Spark requires manual setup and management.

# Main Use Cases:
1. Data Engineerig (ETL pipelines): Designing and building data pipelines and infrastructure
2. Data Warehousing: Involves collecting, storing and managing structured data for analysis and reporting.
3. Machine Learning: Customize large language models (LLMs) using your own data.

# Components
1. Workspace: Data Bricks project.
2. Catalog: Centralized Metadata and user management across workspaces. 
3. Workloads: Configure ETL processes.
4. Compute: Set up the compute that will run the pipeline.

# Apache Spark Vs Data Bricks

| **Step**                          | **Apache Spark (Traditional Setup)**                              | **Azure Databricks**                                               |
|------------------------------------|-------------------------------------------------------------------|-------------------------------------------------------------------|
| **1. Infrastructure Setup**        | Install and configure Spark, Hadoop, and dependencies on servers. | Automated cluster provisioning and management.                    |
| **2. Cluster Management**          | Manually manage cluster scaling, node failures, etc.              | Auto-scaling and built-in cluster management.                     |
| **3. Data Ingestion**              | Use tools like Kafka, Flume, or custom scripts to ingest data.     | Built-in connectors to various data sources (Azure Blob, SQL DB, etc.). |
| **4. Data Processing**             | Use Spark APIs (PySpark, Scala, Java) for batch and stream processing. | Simplified Spark APIs with optimized runtimes.                    |
| **5. Resource Allocation**         | Manually configure resource allocation (RAM, CPU, etc.).           | Dynamic resource allocation with optimized performance.           |
| **6. Job Scheduling**              | Use third-party tools (e.g., Apache Airflow, Oozie) for scheduling.| Integrated job scheduling with Databricks Jobs.                   |
| **7. Monitoring and Logging**      | Set up third-party tools (e.g., Prometheus, Grafana) for monitoring.| Built-in monitoring and logging in the Databricks UI.             |
| **8. Collaboration**               | Limited collaborative features; version control via Git.           | Notebooks with real-time collaboration, versioning, and sharing.  |
| **9. Security**                    | Manual configuration for authentication and encryption.            | Integrated with Azure AD, role-based access control, and encryption. |
| **10. Deployment & Automation**    | Custom CI/CD pipelines required for deployment and updates.        | CI/CD integration with Azure DevOps or other services.            |

Azure Databricks streamlines many aspects of Spark-based data pipelines, providing a managed service that automates infrastructure, job scheduling, and collaboration, reducing manual effort required in traditional Apache Spark setups.

# Data Bricks: ETL Data Pipeline(overview)
1. Extract(Ingest): Connect to data sources (e.g., databases, APIs, or cloud storage) and ingest raw data into Databricks using Databricks notebooks or automated jobs.
2. Transform: Use Apache Spark in Databricks to clean and transform the data. This may include filtering, aggregating, joining, and applying business logic.
3. Load: Write the transformed data into a target destination, such as a data lake, data warehouse, or other storage systems (e.g., Delta Lake, Azure SQL, or Snowflake).

# Data Bricks: CI-CD
![dbrks-cicd](https://github.com/AleMorales9011/ForgeWare/blob/9800bc00153d62246cda7550e554a405b9bd0525/src/images/dbkrs-cicd-001.jpg)

The image shows a **CI/CD pipeline** for deploying Databricks jobs in Azure Databricks. Here’s a breakdown of the process:

1. **Development and Testing**: 
   - Developers create and test data pipelines in the **Dev & Test** environment within **Azure Databricks**.
   - After the data pipelines are developed, the **CI pipeline** is triggered.

2. **CI Pipeline (Continuous Integration)**:
   - **Run Unit Tests**: The pipeline runs both local unit tests and remote notebook tests (using tools like Nutter).
   - **Publish Artifacts**: After successful tests, the artifacts (output of the tests or notebooks) are published.
   - The CI pipeline concludes by triggering the **CD pipeline**.

3. **CD Pipeline (Continuous Deployment)**:
   - **Deploy to STG**: Databricks jobs are deployed to the **STG (Staging)** environment in Azure Databricks.
   - **Run Integration Tests**: After deployment, integration tests are run in the staging environment.
   - **Deploy to PROD**: If integration tests are successful, the Databricks jobs are deployed to the **PROD (Production)** environment in Azure Databricks.

# Next Steps
Learn more about Azure Databricks, a unified analytics platform for data analysts, data engineers, data scientists, and machine learning engineers at [Azure Databricks Documentation](https://learn.microsoft.com/en-us/azure/databricks/)
