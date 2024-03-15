

# Create a new repository on the command line

echo "# myrepo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/username/reponame.git
git push -u origin main


# Pushing an existing repository from the command line


git remote add origin https://github.com/username/reponame.git
git branch -M main
git push -u origin main

# Pull with Rebase (git pull --rebase):

This command fetches the latest changes from the remote repository and then attempts to replay your local commits
on top of the updated remote branch head.

git pull origin <branch_name> --rebase
