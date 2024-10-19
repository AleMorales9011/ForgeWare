# Azure Databricks: Data Pipeline Deployment

60 minutes - DevOps - Data Engineering

In the realm of big data, machine learning algorithms require pre-processed data to perform calculations and generate meaningful results. Take, for example, a product or video recommendation algorithm. For it to function effectively, it must store and process vast amounts of user interaction data, such as viewed, saved, and liked products. This data is then compared in real-time with similar data from other users. By applying probabilistic algorithms, the system identifies common patterns and ultimately delivers personalized product recommendations to the user.

# Data Pipelines
A data pipeline is a series of processes that automate the movement and transformation of data from one system to another, ensuring that raw data is efficiently converted into actionable insights.

# Apache Spark
Apache Spark is an open-source, distributed computing system that provides fast, in-memory data processing capabilities for big data workloads, supporting tasks like batch processing, machine learning, and stream analytics.

# Data Bricks
Databricks is a managed, cloud-based platform built on Apache Spark that simplifies Spark's deployment, scaling, and collaboration, offering additional features like auto-scaling, integrated notebooks, and seamless integration with cloud services, while Apache Spark requires manual setup and management.

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

# Data Bricks: Data Pipeline Deployment
Below there's a clear, structured approach to automating data workflows, ensuring efficient data ingestion, processing, and storage to help understand how to leverage Databricks’ capabilities.

# Step 1: Infrastructure Set UP
Infrastructure setup in Azure Databricks involves provisioning managed clusters, integrating with Azure services like storage and security, and configuring the environment for seamless data processing and analytics with minimal manual intervention.

```bash
#!/bin/bash

# Set Databricks configuration details
DATABRICKS_HOST="https://<databricks-instance>.azuredatabricks.net"
DATABRICKS_TOKEN="<your-databricks-api-token>"

# Configure the Databricks CLI with host and token
databricks configure --token <<EOF
$DATABRICKS_HOST
$DATABRICKS_TOKEN
EOF

# Create a Databricks cluster
databricks clusters create --json '{
  "cluster_name": "my-sample-cluster",
  "spark_version": "15.4.x-scala2.12",
  "node_type_id": "Standard_D3_v2",
  "autoscale": {
    "min_workers": 2,
    "max_workers": 8
  },
  "autotermination_minutes": 60,
  "spark_env_vars": {
    "PYSPARK_PYTHON": "/databricks/python3/bin/python3"
  }
}'

# Output message to indicate cluster creation request has been submitted
echo "Cluster creation request submitted."
```

# Step 2: Cluster Management
Databricks cluster management automates the creation, scaling, and termination of clusters, optimizing resources and performance while allowing users to easily configure and monitor clusters for data processing and analytics tasks.
> Note: For it to work the min require of compute resources are needed. So, it's nescessary to check the azure subscription compute quotes in the region where the databricks resource
> live otherwise the cluster will not be created. Resources can be requested via a "resource request" made to azure.

```json
{
    "autoscale": {  // Configuration for auto-scaling the cluster
        "min_workers": 2,  // Minimum number of workers (nodes) that the cluster will scale down to when demand is low
        "max_workers": 8   // Maximum number of workers the cluster can scale up to during peak load
    },
    "cluster_name": "alejandro Morales's Cluster",  // The name of the cluster for identification in Databricks
    "spark_version": "15.4.x-scala2.12",  // The version of Spark being used (15.4.x) along with the Scala version (2.12)
    "spark_conf": {},  // Placeholder for additional Spark configurations (empty in this case)
    "azure_attributes": {  // Azure-specific attributes for cluster deployment
        "first_on_demand": 1,  // The first worker node is an on-demand instance, ensuring quicker startup
        "availability": "ON_DEMAND_AZURE",  // Specifies that the cluster will use Azure on-demand VMs
        "spot_bid_max_price": -1  // No maximum price is set for spot instances; will use the default spot pricing if spot instances are used
    },
    "node_type_id": "Standard_D4ds_v5",  // Specifies the type of VM instance used for the workers (Standard_D4ds_v5 in this case)
    "ssh_public_keys": [],  // List of SSH public keys to allow SSH access to the cluster nodes (empty, so no SSH access configured)
    "custom_tags": {},  // Custom tags for organization or categorization (none are set here)
    "spark_env_vars": {  // Environment variables for Spark, specifying the Python version to be used
        "PYSPARK_PYTHON": "/databricks/python3/bin/python3"  // Path to Python 3 for running PySpark jobs
    },
    "autotermination_minutes": 120,  // Cluster will automatically shut down after 120 minutes of inactivity to save costs
    "init_scripts": [],  // List of initialization scripts to run when the cluster starts (empty in this case)
    "single_user_name": "alemorales9011@gmail.com",  // The user who owns the cluster and is allowed access
    "data_security_mode": "SINGLE_USER",  // Specifies that the cluster is in single-user mode, enhancing data security by restricting access to one user
    "runtime_engine": "PHOTON"  // Specifies the use of the Photon runtime engine, which is optimized for faster query execution
}

```
# Step 3: Data Ingestion


