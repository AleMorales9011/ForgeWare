
### Cloning a repository

> [!TIP]
> Helpful advice for doing things better or more easily.

![cloning a repo](https://github.com/AleMorales9011/01-DEVOPS-AWS/blob/a65ea31dc0630f24838b822e52372302da1cab12/002-GIT-CREATING%20%26%20PUSHING%20REPOSITORIES/cloning%20a%20repo.jpg)

---
### Create a new repository on the command line

```bash

echo "# myrepo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/username/reponame.git
git push -u origin main

```
---
### Pushing an existing repository from the command line

> [!IMPORTANT]
> command example

![git-command](https://github.com/AleMorales9011/01-DEVOPS-AWS/blob/35bb6643e1b540ecf2530230dd3fb847c47bde02/002-GIT-CREATING%20%26%20PUSHING%20REPOSITORIES/git-command.jpg)
```bash

git remote add origin https://github.com/username/reponame.git
git branch -M main
git push -u origin main

```
---
### Pull with Rebase (git pull --rebase):

>This command fetches the latest changes from the remote repository and then attempts to replay your local commits
>on top of the updated remote branch head.

```bash

git pull origin <branch_name> --rebase

```
