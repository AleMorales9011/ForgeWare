
# Version Control Basics:  
After the adding the new hires to it's server to support the business growth in the previous chapter. Jane, the owner of "Crafty Corner," has been juggling product photos, descriptions, and inventory through a mess of spreadsheets and email threads. 

**It's become a nightmare to keep track of everything**. Employees are changing descriptions, photos, changing prices and adding discounts and now Jane doesn't know th timeline of events. She doesn't know if the discounts were beneficial or not or which product desription is best or why changes were made in the first placce or by who. 

![Git](https://img.shields.io/badge/GIT-E44C30?style=for-the-badge&logo=git&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-35495E?style=for-the-badge&logo=ubuntu&logoColor=2CA5E0)

## Methodology
To show a step-by-step process of how to use Git for version control management through a fictional situation. 

## Table of Contents
- Installing Git (One-time setup)
- Initializing a Git repository
- Managing Data with Git
- Committing Changes:
- Reverting Mistakes (Optional)
- Keeping Track of Progress
- Remote Access
- Remote Acces using a Bare Git Repository
- Remote Acces using a Git Web Hosting Service (GitHub)
- Conclussion



## Install Git (One-time setup):
*Windows/macOS:* Download and install Git from the official website ```https://git-scm.com/downloads.```
*Linux:* Git is usually pre-installed on most Linux distributions. You can check by opening the terminal and typing ```git --version```. If not installed, use your package manager ```(e.g., sudo apt install git on Ubuntu)```. 

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

## Committing Changes:

After adding any updated files, Jane can create a snapshot of her work with a descriptive message using: ```git commit -m "Updated scarf description with new color options"```

```ruby
git commit -m "My first commit"
```
The -m flag lets you add a commit message describing the changes.

## Reverting Mistakes (Optional):

Oops! Jane accidentally deleted a photo. No worries! She can use Git to go back to the previous commit with:

```ruby
git checkout HEAD~1
```
This command "checks out" the previous commit (represented by HEAD~1).

## 4. Keeping Track of Progress:

Jane can view the history of her commits with:

```ruby
git log
```
This shows a list of commits with their messages, allowing her to see how her data has evolved over time.

## Remote Acces
In the previous scenario Jane and its employees use git to collaborate using Git within the same server. Now, Jane has bought another computer so the operations deparment could make changes such as adding products, client informations and documents like contracts from their own work station. 

>[!Note]
> The most common way to ue Git to collaborate is using remote acces to online hosting repositories such as Github, Gitlab or Azure Repo.However this is not the only way. In the following example Jane's employee will acces Crafty Corner repo from his operation work station.


## Remote Acces using a Bare Git Repository
### Server-side:
Connect to your server and use 
```ruby
git init --bare <repository_name>.git # to create a bare repository directory (e.g., project.git).
```
### Client-side (Local Machines):
Users can then clone the repository using 
```ruby
git clone ssh://server_username@server_ip/path/to/repository.git #(replace placeholders with your info).
```
After making changes locally, they push their commits with ```git push origin main``` (assuming the remote is named origin and the branch is main).

## Remote Acces using a Git Web Hosting Service (GitHub) 

### 1 Clone the main repository:

```ruby
git clone <URL of Jane's repository>
```
This downloads a copy of the entire repository, including all branches and history, to the employee's local machine.

### 2 Make changes and add files:

The employee can use standard Git commands like:
```ruby
git add <filename> # to stage specific files for commit.
git commit -m "Meaningful commit message" # to create a snapshot of their changes with a descriptive message
```
### 3 Renaming your branch 
```ruby
git branch -M main
```
By default, Git creates a branch named "master" when you initialize a repository. This command renames the current branch (which points to the "first commit") from "master" to "main".

### 4 Configuring a remote repository

```ruby
git remote add origin <repo URL> # This command configures a remote repository.
```

### 5 Push changes directly (Use with Caution):
```ruby
git push origin <branch_name>
```
This command pushes the employee's local commits directly to the remote repository. Here:
```origin``` is the default shortcut for the remote repository.
```<branch_name>``` specifies the branch they want to push their changes to (usually master for the main branch).

>[!Note]
> Pull with Rebase (git pull --rebase):
Sometimes when pushing changes you can get an error. Usually means that the remote branch is ahead of yours. So you need to pull changes first before push your new changes. ```git pull --rebase``` fetches the latest changes from the remote repository and then attempts to replay your local commits on top of the updated remote branch head.

```ruby
git pull origin <branch_name> --rebase
```
# Conclussion
This Git tutorial has equipped you with the essential tools to manage your code effectively. By mastering these core Git concepts, you've unlocked a powerful way to manage projects, track progress, and collaborate efficiently. This foundation will serve you well as you explore more advanced Git features and delve deeper into the world of version control. Feel free to contribute! If you have suggestions, corrections, or want to share your own Git tips, feel free to submit a pull request to this repository.
