# Git usage guide

As with most software development teams, we will be using git as our version control system. All of our code is stored within git repositories, spread between Bitbucket (an Atlassian product much like Github) and Github. In an effort to streamline development and better track where our changes have gone, I will detail the different types of branches we will be using.

Take a look at this image, borrowed from Vincent Driessen’s “[A successful git branching model](https://nvie.com/posts/a-successful-git-branching-model/)”:

![Git branching model](git-model-2x.png "Git branching model")

This image shows us the bird’s-eye view of how we will develop, merge, and deploy in our git repository.

Let’s look at each of the branches more closely.

**master**

The `master` branch (hereafter referred to as just `master`) will always be the base branch, or the trunk of the tree, from which we will create all of our other branches. The code on `master` is the code that’s currently live on our production server. Whenever we deploy our code to production, it will always come from `master`. Before we deploy, we will tag the commit with the current version number. If we find critical bugs on `master` that need to be fixed quickly, we will create a “hotfix” branch, fix the bug, and merge it back into `master`. It will also need to be merged into `develop`.

**develop**

The other branch that you’ll become very familiar with is `develop`. `develop` is the branch from which we will create our feature branches and release branches. `develop` contains the latest version of the code we are actively developing.

**Feature branches**

Feature branches are where you will do all of your development. When you are ready to work on a new feature, create a branch off of develop. The branch will be named according to the ID of the story or task you’re working on. In a project management tool such as Jira, this ID will look something like “&lt;project>-1234” where &lt;project> is the name of your project. If you are not using a project management tool that assigns IDs, use the title of the story or task.

The name should be all lowercase, start with “feature-”, and have hyphens instead of spaces. For example, if the story/task ID is “ABC-1234”, the branch name should be something like `feature-ABC-1234`. 

If you are using the title instead of the ID, the branch name should be something like `feature-add-timezone-field-to-users`. If the title looks a little long, you can abbreviate, remove, or combine some of the words (“feature-add-timezone-users”).

When you have finished developing and testing the feature, create a pull request and select `develop` as the branch you’ll be merging into. Once the pull request has been approved, the branch will be merged into `develop` and deleted.

For more information on how to set up a pull request, refer to [this guide](development_pipeline.md).

**Release branches**

Release branches are created whenever we are about to deploy a release. A release can be as big as a complete rewrite or as small as changing a color in a css file. The name of a release branch will be the current version number, adding one to the Major, Minor, or Revision number, depending on the type of release. For more information on versioning and how version numbers are formatted, refer to [this guide](versioning.md).

Let’s look at an example. Let’s say the current version of our application is 1.3.1. This means we are in our first major release, our third minor release, and our first revision. Now, we’ve decided to deploy a new release with two new features. Because we’re only deploying two new features, and because this isn’t one of our quarterly releases, this qualifies as a “revision”. So we will add one to the revision number. Now our version number is 1.3.2. We create a branch off of `develop` and name it `1.3.2`. After we QA and fix any bugs, we merge `1.3.2` into `master`, tag the commit “&lt;project_slug>-1.3.2” where &lt;project_slug> is the slug of the project name, and deploy our code.

Make sure that we are only retaining the last three release branches in the repository. This means that if we just released 1.3.2, keep the 1.3.2 branch and the two that immediately preceded it, and make sure any older branches are deleted.

**Fix branches**

Fix branches are created when a bug is found in the release branch during testing. One branch will be created for every defect logged in our task management software relating to a story or task from the pending release.

If the pending release branch is called `1.3.2`, create a branch off of `1.3.2` and name it fix-&lt;task_id>, where &lt;task_id> follows the same conventions as in our other branch types: all lowercase and hyphens instead of spaces. For example, if the bug ID is “ABC-9012”, the name of the hotfix branch should be something like `fix-ABC-9012`.

When you have finished developing and testing the fix, use the same process as you would with a feature branch, only this time select the release branch (in this case, `1.3.2`) as the branch you’ll be merging into. Once the pull request has been approved, the branch will be merged into `1.3.2` and deleted.

**Hotfix branches**

Hotfix branches, like fix branches mentioned above, are created when a bug is found. The key difference here is that hotfixes are for fixing critical bugs found on `master`, bugs that affect the core usability of the application and need to be fixed immediately. Often, we will create a ticket or a bug card in our task management software that details the bug and how to reproduce it. To start working on the hotfix, create a branch off of `master` and name it “hotfix-&lt;task_id>” where &lt;task_id> follows the same conventions as in our other branch types: all lowercase and hyphens instead of spaces. For example, if the bug ID is “ABC-5678”, the name of the hotfix branch should be something like `hotfix-ABC-5678`.

When you have finished developing and testing the hotfix, use the same process as you would with a feature branch, only this time select `master` as the branch you’ll be merging into. Once the pull request has been approved, the branch will be merged into `master`. Tag this latest commit with the new version number. The branch will then be merged into `develop` before being deleted.
