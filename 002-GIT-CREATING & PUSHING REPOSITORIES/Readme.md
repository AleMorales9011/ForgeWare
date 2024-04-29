
# Abstract
After the adding the new hires to it's server to support the business growth in the previous chapter. Jane, the owner of "Crafty Corner," a charming online craft store, has been juggling product photos, descriptions, and inventory through a mess of spreadsheets and email threads. It's become a nightmare to keep track of everything, especially with her growing product line. Employees are changing descriptions, fotos, changing prices and adding discounts and now Jane doesn't know th timeline of events. She doesnt know if the discounts were beneficial or not or which product desription is best or why changes were made in the first placce or by who. 

![Git](https://img.shields.io/badge/GIT-E44C30?style=for-the-badge&logo=git&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-35495E?style=for-the-badge&logo=ubuntu&logoColor=2CA5E0)

## Methodology
Jane decide to use Git ( a version control tool) to solve the problem. Git promotes efficient collaboration, and a clear development history. Multiple employees can work on the same folder simultaneously. Git allows them to **create separate branches** for their modifications, **preventing conflicts**. Git also tracks every change ever made. So now Jane can know who did what and when. And measure the impact of changes.

## Install Git (One-time setup):
Windows/macOS: Download and install Git from the official website ```https://git-scm.com/downloads.```
Linux: Git is usually pre-installed on most Linux distributions. You can check by opening the terminal and typing ```git --version```. If not installed, use your package manager ```(e.g., sudo apt install git on Ubuntu)```. 

## Initialize a Git repository:

Open a terminal window and navigate to the folder where Jane wants to store her "Crafty Corner" data using the ```cd command (e.g., cd Documents/CraftyCorner).``` Then, type the following command to create a new Git repository:

```ruby
git init
```
This creates a hidden folder called .git where Git stores all its information.

## Managing Data with Git
Once the repository is set up, Jane can start using Git commands to manage her data:

Adding Changes:
```ruby
git add
```
Let's say Jane updates a product description for a knitted scarf in a text file named scarf_description.txt. To tell Git to track this change, she can use: ```git add scarf_description.txt```

This "stages" the file for the next commit.

## Create a new repository on the command line

```ruby

git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/username/reponame.git
git push -u origin main

```

### Pushing an existing repository from the command line

> [!IMPORTANT]
> command example

![git-command](https://github.com/AleMorales9011/01-DEVOPS-AWS/blob/35bb6643e1b540ecf2530230dd3fb847c47bde02/002-GIT-CREATING%20%26%20PUSHING%20REPOSITORIES/git-command.jpg)
```ruby

git remote add origin https://github.com/username/reponame.git
git branch -M main
git push -u origin main

```
---
### Pull with Rebase (git pull --rebase):

>This command fetches the latest changes from the remote repository and then attempts to replay your local commits
>on top of the updated remote branch head.

```ruby

git pull origin <branch_name> --rebase

```
