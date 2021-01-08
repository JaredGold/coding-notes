# Git

#### How Does Git Work?

Git is a collection of snapshots of a file. Git saves every step you save at the time of a commit.

The directory you are working in when initialised creates a .git directory.

This is a local repository. If you want to make it a main repository you can push it to a remote repository.

#### Git Branches

A branch is a pointer to a commit/snapshot

`master` is the default branch

When you make a new branch you just make a new pointer.

##### Why Branch?

We branch to make clairty when we make source code changes in different contexts.

It can also be used on Bug fixes or different releases of our code.

#### HEAD Pointer

Head pointer shows us what branch we are currently using.

The below shows a list of branches.

``` 
> git branch
* master
> git checkout feature1
```

#### Creating a branch

* Create a branch

  `git branch <branch_name>`

* Move HEAD to a branch:

  `git checkout <branch_name>`

* Create a branch and move HEAD to it in one command:

  `git checkout-b <branch_name>`

#### Undo

There are ways to change and undo a mistake made on your local repository.

To undo an unstaged change (`git add`)

1. Check `git status` and check to make sure they are not staged.
2. If the file is unstated run `git checkout -- <file>`. This can be used as a list or even as an all `.`
3. Run `git status` to make sure there are no unstaged changes.

If you've run a `git add`

1. check `git status` see if they are added. If they are:
2. `git reset HEAD` will unstage any changes that haven't been commited and reset the head back to the original spot it was. You can choose specific files as well by adding the file after `...HEAD <file>`
3. `git status` to make sure it is

If you've commited to your local repository.

1. If it has not been pushed. `git reset HEAD~1` Which says I want to reset `HEAD` to the commit prior to the last one I made.
2. Important to note this will put the changes in the `git status` if you want to wipe the changes use `git checkout -- <file>` as above.

## Git Remote Repo

**Local** repo's are what reside on the computer system. 
**Remote** Repo's are saved online. They can be set on any server but mainly done through GitHub

### What comes first? Local or Remote?

*Either comes first depending on the Scenario.*

* Scenario 1:
  * Create local repository with `git init`
  * Create empty remote repository on GitHub
  * Use `git remote add` to connect the local to the remote repository
* Scenario 2:
  * A populated remote repository exists
  * Use `git clone` to copy the remote repository to the local machine

#### Git Remote Command

* show remote connections:
  * `git remote -v`
* Add remote connection:
  * `git remote add name remote-repo`

This looks like: `git remote add origin git@github.com:supercoder/my-app.git`

#### Cloning a Git

`git clone git@github.com:/supercoder/my-app2.git`

A repository that is not on the computer yet can be cloned *(copied)* as above.

This also creates a connection called `origin` to the remote repo.

#### Origin

Origin is the default name to the connection of the primary remote repository.
You could use any name it the convention is origin.

`git clone` autimatically makes a connection called origin.

#### Changing Remote Connections

You can change name and URL as well as remove remote connections using remote connection.

### Keeping repositories in Sync

Local repositories are great because it means that if we need to change anything we can quite fast and easily but if you lose the laptop and want to pull the repo you need it to be remote.

* Generally you want to keep the local master in sync with the origin (remote) master branch
* After any change is made by any dev to the remote repo master branch you want to pull the changes from master to sync

``` 
$ git checkout master
On branch master
$ git pull origin master
```

#### Pull vs fetch

`fetch` and `pull` both grab the latest data

* `pull` does a `fetch` and `merge`, merging any changes from the remote branch into the working branch
* `fetch` only retrieves the latest information from the remote branch and must be followed by a `merge` to include those changes in the working directory.

You would use fetch if you were ansure if you wanted to make the changes.

#### When to synch?

If your local master is older the Remote repos master/origin then before merging our feature on the master branch you want to pull the latest commit from the master to merge it into the master and test it to make sure there are no merge conflicts.

## Sharing Your Work

#### Push

* To share the work done we need to `push` it to a remote repo
* Until you push it no one can see or use it
* You have to push to some remote branch to raise a pull request

#### Pull Request (PR)

You must first push before you can pull. There needs to be an initiation on GitHub

You can open a pull request at any point during the dev process.

* when you have little or no code but want to share some screenshots or general ideas
* when you're stuck and need help or advice
* when you're ready for someone to review your work

Pull requests can be from a feature branch or a forked master branch.

#### Pull requests - getting feedback

Using `@username` system in your Pull Request message to ask feedback from specific people or teams.

Pull requests comments are written in Markdown, This means we can get heaps of detail, emojiis, images and others.

You can add reviewers to the pull request.

Any commit on the target branch after the PR is raised will be added to the PR

(CODE REVIEWS)



#### Merge Pull Request

* Once the PR is reviewed and approved it can be merged
* Merging creates a new merge commit with a comment that it is a merge of the pull request
* Squash and merge will squash all commits in the PR into a single commit
* Rebase and merge will rebase the commit (only if it's safe)