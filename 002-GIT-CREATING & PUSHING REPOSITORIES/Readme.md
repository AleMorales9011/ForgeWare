
# Abstract
Git **streamlines the software development process** for companies by promoting efficient collaboration, code safety, and a clear development history. Multiple developers can work on the same codebase simultaneously. Git allows them to **create separate branches** for their modifications, **preventing conflicts** and ensuring a stable main code. Git also tracks every change ever made to the code. This allows companies to revert to previous versions if necessary, or see how a specific feature evolved. In addition if a critical error is introduced, Git **allows developers to roll back** to a working version of the codebase, minimizing downtime and data loss.


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
