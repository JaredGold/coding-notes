# Git Collaboration

#### Forking workflow

A forking workflow is when a developer has their own cloned server-sided clone.

1. Clone main repo
2. Pull clone repo to comp
3. Make changes on personal computer
4. Push to your repo
5. Push your repo to the main repo

A forking workflow is nevvesary for largem organic and distrubutes teams to safely contribute to a repository. It is perfect for open source projects.

It is unnecessary for private projects with well-defined teams.

1. Fork central project repo
2. Clone fork (will creat origin connection to fork)
3. create upstream connection on local repository

#### Workflow Steps

1. Sync with central project repo master
2. Create a feature branch
3. Implement, test, commit (on branch)
4. Make sure still in sync with central project master
5. Push to fork (on branch)
6. Raise pull request on central project repo from fork
7. Request is reviewed and merged into central project repo
8. Delete branches (optional)

Full code

1. `git pull upstream master`
2. `git checkout -b feature1`
3. `git add .; git commit -m "feature 1 done"`
4. `git checkout master; git pull upstream master`
   `git checkout feature1; git merge master`
5. `git push origin feature1`
6. Raise Pull Request from my fork
7. Merge Pull request



## Code Review

It's important to review each other's code to make sure we don't make common human mistakes.

#### What to look for in review

* Does the existing tests pass? (what tests you run will depend)
* Is the logic correct?
* Are the requirements met?
* Are new/updated test cases included and sufficient?
* Is the code consistent with the style guides? (should be automated as much as possible)

#### What to keep in mind when you review

When you are thinking of adding code review comments, first ask yourself

* Is it true?
* Is it necessary?
* Is it kind?

Use code review as a teaching and learning opportunity that makes the code better, your clients happier, and your team stronger and better



#### How to do the review

1. Checkout the remote branch to your local machine
2. Review and test the code locally
3. Make any comments on the pull request, and either
   * Approve
   * Request changes
4. Delete the branch when you are done with the review process