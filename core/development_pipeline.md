# Development pipeline

This document will detail how features are developed for our applications. First, we will talk about how we determine what needs to be worked on. Then we will talk about how we go from a card in our task management software to a deployed feature.


### What are we working on?

As with other development teams, we operate in sprints. In our case, we use the traditional two week sprints. This means that we are deploying some number of features every two weeks, hopefully finishing our assigned tasks at the end of a sprint and starting new tasks at the beginning of the next sprint.

Before any work can be done, stories and tasks need to be written. Stories are normally written by our project manager, with the help of the client and sometimes a developer. If you are familiar with the Agile methodology, then the term “story” will be familiar to you. They are more user-centered and high-level. Tasks are normally written by a developer and are more technical. For both stories and tasks, we will attach all relevant documentation and assign either effort points or estimated hours of work (for a story, this can be the sum of all its task points).

For more information on these Agile issue types and how we use them, refer to the [Agile overview](agile_overview.md) document.

### How do we do our work?

First, we select a story or task from our task management software. In our case, this is Jira. Depending on the project, you may pick a story yourself or you may be assigned one. The assignment of these stories usually happens in a sprint planning meeting. On the Kanban board in Jira, navigate to the row with your name and avatar. Drag the story/task from the To Do column to the Doing column when you are going to start working on it.

Next, create a feature branch for the story. Refer to the [git usage guide](git_usage_guide.md) for more information on branches and how to name them.

Check out the branch to your machine and start coding. When you are done, make sure you have written unit tests as well as functional tests that can demonstrate the fulfillment of the requirements of the task(s). In the (hopefully) small change that you don’t have automated testing set up: write out tests as instructions in the story ticket, or in a separate "testing ticket".

If all of your tests pass, and you’ve rerun all other existing tests successfully, submit a pull request with the target branch as `develop`. Title the pull request similarly to the story/task title. Write a brief description of the changes you have made. The system should have pulled in your commit messages into the description field, so feel free to use these; just make sure it succinctly describes the changes you have made. Select the lead developer as a reviewer and, if possible, one other developer. In Jira, move your story/task to the QA column.

The lead developer and the other reviewers will checkout your branch, run the tests, and inspect your code. At first, this may seem daunting, having other people review your code. But this ensures that everyone’s code is held to the same standard. Everyone will have a chance to review someone else’s code. By allowing others to review your code, they may catch something that you missed, and this is a great opportunity to learn new things from your peers. To leave feedback on the code, create a comment on the pull request on the relevant lines. Common forms of feedback include pointing out a bug, suggesting (and sometimes providing) new code, asking a question about the code, or asking for removal of the code (e.g., if you repeated the line earlier and it was redundant). You are welcome to reply to the comments or to simply implement the suggested changes.

If changes are suggested and you would like to implement them, make the changes in your branch, run the tests to make sure everything is still working, and push the branch. The pull request will automatically update, and the reviewers will pull the branch and check your work again.

At this point, if everything looks good, the reviewer should approve the pull request. A successful pull request is one where all reviewers approved. The final say, however, will be from the lead developer. Once the lead developer approves, they will merge the branch into develop, close the pull request, and delete the feature branch. Your story/task is now considered done, so go to Jira and move the story/task to the Done column.

That’s it!

If later you realize you forgot something or you found a bug, and you are in between releases, feel free to create a branch off of `develop`, fix what you need to fix, and submit another pull request.
