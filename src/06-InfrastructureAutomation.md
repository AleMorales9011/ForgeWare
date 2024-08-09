![banner](images/banner_9.jpg)
# Automating Web App deployment with Bash

Manually deploying a web server involves running several commands in a specific order. A `Bash script` can automate these steps, saving you time and effort, especially if you need to deploy Apache on multiple servers.

# Web Server Deployment

This Bash script provides a streamlined and automated approach to deploying an `Apache` web server.

```ruby

#!/bin/bash
----------------------------------------------------------------------------------
echo "Updating and installing apache2 and unzip..."
apt-get update
apt-get upgrade -y
apt-get install apache2 -y
apt-get install unzip -y
----------------------------------------------------------------------------------
echo "Getting the website from a remote repo..."
cd /tmp
wget https://github.com/denilsonbonatti/linux-site-dio/archive/refs/heads/main.zip
----------------------------------------------------------------------------------
echo "Unziping the file and pasting into the Apache directory..."
unzip main.zip
cd linux-site-dio-main
cp -R * /var/www/html/
----------------------------------------------------------------------------------

```

# Conclussion

Scripts ensure consistency, reduce errors, and save time compared to manual deployments. The `script` can be easily customized to fit your specific needs and integrated into larger automation workflows.

