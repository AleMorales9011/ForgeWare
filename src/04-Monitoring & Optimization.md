![banner](images/1.jpg)
# Performance & Optimization

By monitoring container performance metrics like CPU, memory, and network usage, you can identify and troubleshoot issues before they impact users. This proactive approach helps prevent outages and ensures high service quality for your applications.

# Requirements

1. Docker: Container management
2. Prometheus: Scrapes metrics
3. Node Exporter: Export metrics
4. cAdvisor: Scrapes specific metrics for containers
5. Grafana: Build dashboards for monitoring

# Folder Structure

A well-defined structure promotes modularity.  Each service or component can reside in its directory, encapsulating its configuration files, Dockerfile, and related scripts.  This promotes reusability and independent development of each service.

```bash
#! bin\bash

echo "Creating Folder Structure"

mkdir -p promgrafnode/prometheus
mkdir -p promgrafnode/grafana/provissioning
touch promgrafnode/docker-compose.yml
touch promgrafnode/prometheus/prometheus.yml

echo "Folder Structure Created"

```

# Grafana

In essence, Grafana empowers you to turn raw data into actionable insights. By providing a centralized platform for visualization, exploration, and alerting, it helps you make data-driven decisions and optimize your systems. 

```yml
version: '3.8' 
networks: 
  monitoring: 
    driver: bridge 
volumes: 
  prometheus_data: {} 
services: 
  node-exporter: 
    image: prom/node-exporter:latest 
    container_name: node-exporter 
    restart: unless-stopped 
    volumes: 
      - /proc:/host/proc:ro 
      - /sys:/host/sys:ro 
      - /:/rootfs:ro 
    command: 
      - '--path.procfs=/host/proc' 
      - '--path.rootfs=/rootfs' 
      - '--path.sysfs=/host/sys' 
      - '--collector.filesystem.mount-points-exclude=^/(sys|proc|dev|host|etc)($$|/)' 
    ports: 
      - 9100:9100 
    networks: 
      - monitoring 
  prometheus: 
    image: prom/prometheus:latest 
    user: "1001" 
    environment: 
      - PUID=1001 
      - PGID=1001 
    container_name: prometheus 
    restart: unless-stopped 
    volumes: 
      - ~/promgrafnode/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml 
      - ~/promgrafnode/prometheus:/prometheus 
    command: 
      - '--config.file=/etc/prometheus/prometheus.yml' 
      - '--storage.tsdb.path=/prometheus' 
      - '--web.console.libraries=/etc/prometheus/console_libraries' 
      - '--web.console.templates=/etc/prometheus/consoles' 
      - '--web.enable-lifecycle' 
    ports: 
      - 9090:9090 
    networks: 
      - monitoring 
  grafana: 
    image: grafana/grafana:latest 
    user: "1001" 
    container_name: grafana 
    ports: 
      - 3000:3000 
    restart: unless-stopped 
    volumes: 
      - ~/promgrafnode/grafana/provisioning/datasources:/etc/grafana/provisioning/datasources 
      - ~/promgrafnode/grafana:/var/lib/grafana 
    networks: 
      - monitoring 
  cadvisor: 
    image: gcr.io/cadvisor/cadvisor:latest 
    container_name: cadvisor 
    ports: 
      - 8081:8080 
    networks: 
      - monitoring 
    volumes: 
      - /:/rootfs:ro 
      - /var/run:/var/run:rw 
      - /sys:/sys:ro 
      - /var/lib/docker/:/var/lib/docker:ro 
    depends_on: 
      - redis 
  redis: 
    image: redis:latest 
    container_name: redis 
    ports: 
      - 6379:6379 
    networks: 
      - monitoring

```
# Service Break-Down: Node exporter

```yaml
# This file defines a Docker Compose service configuration in version 3.8
version: '3.8'

# Define a custom network named "monitoring"
networks:
  monitoring:
    driver: bridge  # Uses the default bridge networking mode

# Define a volume named "prometheus_data" with no configuration (empty dictionary)
volumes:
  prometheus_data: {}

# Define a service named "node-exporter"
services:
  node-exporter:
    # Use the official prom/node-exporter image with the latest tag
    image: prom/node-exporter:latest

    # Set the container name to "node-exporter" for easier identification
    container_name: node-exporter

    # Restart the container automatically unless it's stopped manually
    restart: unless-stopped

    # Mount volumes to expose host system information to the container
    volumes:
      - /proc:/host/proc:ro  # Read-only access to process information
      - /sys:/host/sys:ro    # Read-only access to system information
      - /:/rootfs:ro        # Read-only access to the entire root filesystem

    # Override default paths for collecting metrics within the container
    command:
      - '--path.procfs=/host/proc'  # Set procfs path to mounted host directory
      - '--path.rootfs=/rootfs'    # Set rootfs path to mounted host directory
      - '--path.sysfs=/host/sys'    # Set sysfs path to mounted host directory
      # Exclude specific mount points from filesystem collector (avoids duplicates)
      - '--collector.filesystem.mount-points-exclude=^/(sys|proc|dev|host|etc)($$|/)'

    # Map container port 9100 to host port 9100
    ports:
      - 9100:9100

    # Connect the container to the "monitoring" network
    networks:
      - monitoring

```
# Prometheus

```yml
# This section defines the configuration for a Prometheus container.

prometheus:
  # Defines the image to be used for the container. Here, it uses the official prom/prometheus image with the "latest" tag.
  image: prom/prometheus:latest

  # Sets the user ID inside the container to 1001. 
  user: "1001"

  # Defines environment variables for the container.
  environment:
    - PUID=1001  # Sets the user ID inside the container to 1001 (matches the user specified above).
    - PGID=1001  # Sets the group ID inside the container to 1001 (likely to match the user).

  # Defines the container name to be "prometheus".
  container_name: prometheus

  # Specifies the restart policy for the container. In this case, it will restart only if it stops unexpectedly.
  restart: unless-stopped

  # Defines volumes to be mounted into the container.
  volumes:
    - ~/promgrafnode/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml  # Mounts the local file prometheus.yml from ~/promgrafnode/prometheus directory to /etc/prometheus/prometheus.yml inside the container. This allows configuration file updates without rebuilding the image.
    - ~/promgrafnode/prometheus:/prometheus  # Mounts the local directory ~/promgrafnode/prometheus to /prometheus inside the container. This allows persistence of data collected by Prometheus.

  # Defines the command to be executed when starting the container.
  command:
    - '--config.file=/etc/prometheus/prometheus.yml'  # Specifies the path to the Prometheus configuration file.
    - '--storage.tsdb.path=/prometheus'  # Defines the location for storing time series data collected by Prometheus.
    - '--web.console.libraries=/etc/prometheus/console_libraries'  # Sets the directory containing console libraries.
    - '--web.console.templates=/etc/prometheus/consoles'  # Sets the directory containing console templates.
    - '--web.enable-lifecycle'  # Enables Prometheus web UI lifecycle management features.

  # Defines port mappings for the container.
  ports:
    - 9090:9090  # Maps port 9090 on the host machine to port 9090 inside the container. This allows access to the Prometheus web UI.

  # Defines the network that the container will be connected to.
  networks:
    - monitoring  # Connects the container to the network named "monitoring".


```

