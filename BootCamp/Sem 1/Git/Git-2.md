# Git

Git is a decentralized file working system.

You can work on a git repository without being connected to the internet but you can not save it to an online repository without being connected to the net.



## Create a Repo

* `git init` // Create a local Git Repository
* `git add <file>`  // Add files to the staging index (not commited)
* `git status` // check status of the working tree
* `git commit -m "What you did"` // Commits changes to index

If You are using a remote repository

* `git push`  // push to remote repository
* `git pull` // pull latest changes from remote repo
* `git clone` // Clone Repo into new destination

## Ignore Git

If you would like to tell Git which files you do not want it to save when you add all (`git add .`) You can creat a file called .gitignore `touch .gitignore`

Then you want to open .gitignore the name of the file to the gitignore file.

You can do the same with directory's by adding it the the .gitignore folder `/folder`

You can do all of a type `*.txt`

## Branches

When working on an app you may not want to commit the files to the master working branch. For example if you are working in a team and you are tasked with making the log in screen, you don't want to be working on the master branch or master files and ruin the code for everyone before testing on your own seperate branch which you can name before pushing.

`git branch name-of–branch` - This creates the new branch.

`git checkout name-of-branch` - Changes you to the other branch

When you finish on a branch and want to merge the branches you make sure you are on the branch you want to merge to (master).

`git merge name-of-branch` - will merge the login 

## Remote Repo

Create the repo on Github - Give it a name and description.

Then github will show you a list of everythign you have to do to create a new repo or an existing one. You can use the copy paste there. Below is an example

`git remote add origin https://github.com/test/test.git`

`git push -u origin master`

After linking the two up from that point you could just use `git push`

If you want to update everything from the remote repo (someone made a change and commited it) `git pull`