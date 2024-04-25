## Abstract
Jane, the owner of "Crafty Corner," a small online craft store has been running her business from a single PC. Now she just hired new employees to support the growth of her store. She cannot afford to allow new employees to snoop around her files and data outside the scope of their work, so she needs an organized and structured way to add new users to her server.

![Linux](https://img.shields.io/badge/Linux-000?style=for-the-badge&logo=linux&logoColor=FCC624)
![Ubuntu](https://img.shields.io/badge/Ubuntu-35495E?style=for-the-badge&logo=ubuntu&logoColor=2CA5E0)
![BashScript](https://img.shields.io/badge/bash%20script-0101?style=flat&logo=gnubash&logoColor=%23FFFFFF&labelColor=%23000000)

## Methodology
This script explores basic scripting concepts through practical examples in Bash, a common scripting language for Linux and macOS environments. Sample scripts demonstrate tasks relevant to DevOps, including file manipulation, system administration,

## Result
Diagram for the server's user, directories, and permissions structure.

![IAC](https://github.com/AleMorales9011/01-DEVOPS/blob/3db928f0ef958aa2028429bc991b9a47ed615849/001-USER%2CDIRECTORIES%20%26%20PERMISSION%20STRUCTURE/Basic%20Scripting%20(2).jpg)

Source: Make by the author

```ruby

#!/bin/bash


echo  "Creating directories..."
echo ____________________________________________________

sudo mkdir /public
echo "Directorio `publico` criado"
sudo mkdir /adm
echo "Directorio `adm` criado"
sudo mkdir /ven
echo "Directorio `ven` criado"
sudo mkdir /sec
echo "Directorio `sec` criado"

echo ____________________________________________________

```

