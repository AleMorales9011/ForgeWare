## Infrastructure Automation
Manually deploying a web server involves running several commands in a specific order. A Bash script can automate these steps, saving you time and effort, especially if you need to deploy Apache on multiple servers.

```ruby

#!/bin/bash
----------------------------------------------------------------------------------
echo "Atualizando e instalando apache2 e unzip..."
apt-get update
apt-get upgrade -y
apt-get install apache2 -y
apt-get install unzip -y
----------------------------------------------------------------------------------
echo "Baixando site de repositorio remoto..."
cd /tmp
wget https://github.com/denilsonbonatti/linux-site-dio/archive/refs/heads/main.zip
----------------------------------------------------------------------------------
echo "Descomprimindo arquivo e copiando na pasta do servidor web..."
unzip main.zip
cd linux-site-dio-main
cp -R * /var/www/html/
----------------------------------------------------------------------------------

```
## Conclussion
