## Infrastructure Automation
Manually deploying a web server involves running several commands in a specific order. A Bash script can automate these steps, saving you time and effort, especially if you need to deploy Apache on multiple servers.

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
echo "Unziping the file and pasting into the apache directory..."
unzip main.zip
cd linux-site-dio-main
cp -R * /var/www/html/
----------------------------------------------------------------------------------

```
## Conclussion
This Bash script provides a streamlined and automated approach to deploying an Apache web server. It ensures consistency, reduces errors, and saves time compared to manual deployments. The script can be easily customized to fit your specific needs and integrated into larger automation workflows.

We welcome contributions to this project! Feel free to submit pull requests to improve the script's functionality or add features such as dependency installation or configuration management.
