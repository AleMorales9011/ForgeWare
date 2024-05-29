# Automating the creation of users, permissions, directories, and groups with Bash

There are several advantages to automating the creation of users, permissions, directories, and groups with Bash scripting.

Manually creating these elements can be time-consuming, especially if you need to set up many users with the same configuration. Scripts allow you to automate repetitive tasks, saving you significant time and effort.

## Methodology

This script shows fundamental scripting concepts. It leverages a practical example written in Bash, a prevalent language for Linux and macOS systems.

## Table of Contents

- Payroll Table
- Script
- Permissions Strings
- Conclusion
  
## Payroll Table

Below is the payroll table that Jane from which Jane needs to extract the information to create the user and permissions into the system.

| Employees | Directory         | Group       | Permission                    |
|-----------|-------------------|-------------|-------------------------------|
|Noah       | frontend/public | frontend      | rwx (read,write,execute)      |
|Amelia     | frontend/public | frontend      | rwx                           |
|Bryan      | frontend/public | frontend      | rwx                           |
|Jane       | backend /public | backend       | rwx                           |
|Devin      | backend /public | backend       | rwx                           |
|Bryan      | backend /public | backend       | rwx                           |
|Noah       | ops     /public | ops           | rwx                           |
|Noah       | ops     /public | ops           | rwx                           |
|Noah       | ops     /public | ops           | rwx                           |

### Script

The script below creates the above infrastructure

```ruby

#!/bin/bash

# Creating directories
sudo mkdir /public  # sudo execute the command with superuser privileges
sudo mkdir /frontend     # mkdir is the command for creating a directory
sudo mkdir /backend
sudo mkdir /ops

# Creating groups
sudo groupadd GRP_FRONTEND  # groupadd creates a new group
sudo groupadd GRP_BACKEND
sudo groupadd GRP_OPS

# Creating users for the ADM group
sudo useradd Jane -m -s /bin/bash -G GRP_FRONTEND     # -m: This option tells useradd to create a home directory for the new user. The home directory will be created with the same name as the username.
sudo useradd Devin  -m -s /bin/bash -G GRP_FRONTEND   # -s /bin/bash: specifies the default shell for the new user 
sudo useradd Bryan   -m -s /bin/bash -G GRP_FRONTEND  #  -G: This option adds the new user to a group

# Creating users for the SELLS group
sudo useradd Sarah -m -s /bin/bash -G GRP_BACKEND
sudo useradd Elijah -m -s /bin/bash -G GRP_BACKEND
sudo useradd Maya -m -s /bin/bash -G GRP_BACKEND

# Creating users for the OPS group 
sudo useradd Noah -m -s /bin/bash -G GRP_OPS
sudo useradd Amelia  -m -s /bin/bash -G GRP_OPS
sudo useradd Bryan -m -s /bin/bash -G GRP_OPS

# Specifying permissions for directories
sudo chown root:GRP_FRONTEND /frontend    # chown(change owner) adds the root user as owner of the ADM group 
sudo chown root:GRP_BACKEND /backend
sudo chown root:GRP_OPS /ops

#  Managing permissions
sudo chmod 770 /frontend   # chmod modify the permissions assigned to files and directories in the system.
sudo chmod 770 /backend # 770 is the permission string*  
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

- `Security:` Scripts allow her to define specific user permissions, restricting access to sensitive data outside an employee's designated tasks. This reduces the risk of accidental or intentional data breaches.
- `Efficiency:` Scripts automate repetitive tasks like user creation, saving her valuable time compared to manually configuring each account.
- `Accuracy:` Scripts minimize human error by ensuring consistent configuration for each new user.
- `Organization:` Scripts provide a documented and repeatable process for user management, promoting a clean and organized server environment.
- `Scalability:` As "Crafty Corner" grows, scripts can easily adapt to accommodate additional users without manual intervention.
