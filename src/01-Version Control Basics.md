![Image](images/scene-with-diverse-young-people-being-digital-nomads-working-remotely-from-dreamy-locations.jpg)

# Implementing a version control system with Git/Github  

25 minutes

Version control creates a `history of all changes` made to your files. You can easily revert to previous versions if something goes wrong or you decide you prefer an older iteration. This is like having a `safety net` for your work.

# Table of Contents

1. Installing Git (One-time setup)
2. Clone the main repository
3. Make changes and add files
4. Renaming your branch
5. Configuring a remote repository
6. Push changes
7. Conclusion

# Install Git (One-time setup)

- *Windows/macOS:* Download and install Git from the official website `https://git-scm.com/downloads.`
- *Linux:* Git is usually pre-installed on most Linux distributions. You can check by opening the terminal and typing `git --version`. If not installed, use your package manager `(e.g., sudo apt install git on Ubuntu)`.

# Clone the main repository

```bash
git clone <URL of Jane's repository>
```

This downloads a copy of the entire repository, including all branches and history, to the Devs' local machines.

# Make changes and add files

The Devs can use standard Git commands like:

```ruby
git add <filename> # to stage specific files for commit.
git commit -m "Meaningful commit message" # to create a snapshot of their changes with a descriptive message
```

# Renaming your branch

```bash
git branch -M main
```

By default, Git creates a branch named `master` when you initialize a repository. This command renames the current branch (which points to the `first commit`) from `master` to `main`.

# Configuring a remote repository

This step is necessary to push code to the main repository of the company.

```ruby
git remote add origin <repo URL> # This command configures a remote repository.
```

# Push changes

```ruby
git push origin <branch_name>
```

This command pushes the employee's local commits directly to the remote repository. Here:
`origin` is the default shortcut for the remote repository.
`<branch_name>` specifies the branch they want to push their changes to (usually master for the main branch).

>[!Note]
> Pull with Rebase (git pull --rebase):
Sometimes when pushing changes you can get an error. Usually means that the remote branch is ahead of yours. So you need to pull changes first before push your new changes.

`git pull --rebase` fetches the latest changes from the remote repository and then attempts to replay your local commits on top of the updated remote branch head.

```ruby
git pull origin <branch_name> --rebase
```

# Checking Remote Repositories
This will display a list of all remote repositories associated with your project, along with their URL and fetch/push specifications.
```bash
git remote -v
```

# Erasing a Remote Repository
This will completely remove the specified remote repository from your local project configuration.
```bash
git remote rm <remote_name>
```

# Conclusion

This `Git tutorial` has equipped you with the essential tools to manage your code effectively. By mastering these core Git concepts, you've unlocked a powerful way to manage projects, track progress, and collaborate efficiently. This foundation will serve you well as you explore more advanced Git features and delve deeper into the world of version control.

# Next

We will see how to deploy Infrastructure with Terraform.

