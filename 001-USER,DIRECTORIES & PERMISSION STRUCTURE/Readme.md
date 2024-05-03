## Basic Scripting:
Jane, the owner of "Crafty Corner," a small online craft store has been running her business from a single PC. Now she just hired new employees to support the growth of her store. She cannot afford to allow new employees to snoop around her files and data outside the scope of their work, so she needs an organized and structured way to add new users to her server.

![Linux](https://img.shields.io/badge/Linux-000?style=for-the-badge&logo=linux&logoColor=FCC624)
![Ubuntu](https://img.shields.io/badge/Ubuntu-35495E?style=for-the-badge&logo=ubuntu&logoColor=2CA5E0)
![BashScript](https://img.shields.io/badge/bash%20script-0101?style=flat&logo=gnubash&logoColor=%23FFFFFF&labelColor=%23000000)

## Methodology
This script shows fundamental scripting concepts. It leverages a practical example written in Bash, a prevalent language for Linux and macOS systems. The example focuses on a DevOps-related task, specifically file manipulation within the context of system administration.

## Result
Below is the payroll table that Jane from which Jane needs to extract the information to create the user and permissions into the system.

| Employees | Directory         | Group       | Permission                    |
|-----------|-------------------|-------------|-------------------------------|
|Noah       | operations/public | OPS         | rwx (read,write,execute)      |
|Amelia     | operations/public | OPS         | rwx                           |
|Bryan      | operations/public | OPS         | rwx                           |
|Jane       | adm       /public | ADM         | rwx                           |
|Devin      | adm       /public | ADM         | rwx                           |
|Bryan      | adm       /public | ADM         | rwx                           | 
|Noah       | sales     /public | SALES       | rwx                           |
|Noah       | sales     /public | SALES       | rwx                           |
|Noah       | sales     /public | SALES       | rwx                           |


### Script
The script below creates the above infrastructure 

```ruby

#!/bin/bash

# Creating directories
sudo mkdir /public  # sudo execute the command with superuser privileges
sudo mkdir /adm     # mkdir is the command for creating a directory
sudo mkdir /sales
sudo mkdir /operations

# Creating groups
sudo groupadd GRP_ADM  # groupadd creates a new group
sudo groupadd GRP_SALES
sudo groupadd GRP_OPS

# Creating users for the ADM group
sudo useradd Jane -m -s /bin/bash -G GRP_ADM     # -m: This option tells useradd to create a home directory for the new user. The home directory will be created with the same name as the username.
sudo useradd Devin  -m -s /bin/bash -G GRP_ADM   # -s /bin/bash: specifies the default shell for the new user 
sudo useradd Bryan   -m -s /bin/bash -G GRP_ADM  #  -G: This option adds the new user to a group

# Creating users for the SELLS group
sudo useradd Sarah -m -s /bin/bash -G GRP_SALES
sudo useradd Elijah -m -s /bin/bash -G GRP_SALES
sudo useradd Maya -m -s /bin/bash -G GRP_SALES

# Creating users for the OPS group 
sudo useradd Noah -m -s /bin/bash -G GRP_OPS
sudo useradd Amelia  -m -s /bin/bash -G GRP_OPS
sudo useradd Bryan -m -s /bin/bash -G GRP_OPS

# Specifying permissions for directories
sudo chown root:GRP_ADM /adm    # chown(change owner) adds the root user as owner of the ADM group 
sudo chown root:GRP_SELLS /sales
sudo chown root:GRP_OPS /ops

#  Managing permissions
sudo chmod 770 /adm   # chmod modify the permissions assigned to files and directories in the system.
sudo chmod 770 /sales # 770 is the permission string*  
sudo chmod 770 /ops
sudo chmod 777 /public

```
### Permissions Strings
The permissions string defines a specific access level for the owner, the group, and others on a file or directory.

- 4 represents read only (r = 4 in binary)
- 5 represents read and execute (r = 4, x = 1)
- 7 represents all permissions (read, write, and execute)

**Here's an example to illustrate:**

Consider a permission string -rwxr--r--.

The first character - indicates it's a regular file.
Owner (first set of three): "rwx" - This translates to read, write, and execute permissions for the owner (user who owns the file).
Group (second set of three): "r--" - This translates to read permission only for the group.
Others (third set of three): "r--" - This translates to read permission only for others (users who are not the owner and not in the group).

## Conclusion
By utilizing Bash scripting for user account management on her server, Jane gains several advantages:

- Security: Scripts allow her to define specific user permissions, restricting access to sensitive data outside an employee's designated tasks. This reduces the risk of accidental or intentional data breaches.
- Efficiency: Scripts automate repetitive tasks like user creation, saving her valuable time compared to manually configuring each account.
- Accuracy: Scripts minimize human error by ensuring consistent configuration for each new user.
- Organization: Scripts provide a documented and repeatable process for user management, promoting a clean and organized server environment.
- Scalability: As "Crafty Corner" grows, scripts can easily adapt to accommodate additional users without manual intervention.
