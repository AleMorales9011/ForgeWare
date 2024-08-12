![]()
# System Design

2 hours

System design is the blueprint for a software system. It's about defining the architecture, components, modules, interfaces, and data flow to achieve specific goals.

# Single Server Set Up

A single server setup is a configuration where all components of a system, such as the web server, database, application server, and file storage, reside on a single physical or virtual machine.

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
