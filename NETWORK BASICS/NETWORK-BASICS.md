# DOCKER: NETWORK BASICS
This project provides a collection of **Docker containers** designed to be used together to create a network environment.

The containers are built using industry **best practices** and are configured to work seamlessly together. This readme will provide you with all the information you need to get started using the project, including:

- An overview of the included containers and their functionalities
- Instructions on how to deploy the containers
- How to configure the network
- Usage examples

This project is ideal for **developers and system administrators** who want to quickly and easily set up a network environment for development, testing, or demonstration purposes.

## 01 View Network Interface Details
First, we use the ``ip a`` command to display a comprehensive overview of all network interfaces (like ethernet adapters or Wi-Fi cards) on your system. This includes information like:
- Interface names (e.g., eth0, wlan0)
- IP addresses assigned to each interface
- Subnet masks
- MAC addresses
- Interface flags (up, down, running)

## 02 Check Available Networks
Use ``docker network ls`` It provides a quick and easy way to see all the Docker networks currently running on your system. This includes both the default bridge network created by Docker and any custom networks you've defined.

