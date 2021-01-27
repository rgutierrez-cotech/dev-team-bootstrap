# Agile overview

## Ceremonies

**Sprint Planning**

Sprint Planning happens a day or two before the end of the current sprint. During Sprint Planning, our team reviews the Backlog and decides on a collection of issues to work on for the next sprint. Ideally, all of our work should be generated from issues in the Backlog and previously-decided-on work for our milestones; these issues should be in the Top of the Backlog (a custom sprint that we created to hold upcoming work). But there are other sources of work that may come up.

Part of our workload may be carried over from the previous sprint, but this should be avoided. We should plan well enough to finish our work in the allotted time, but things happen and sometimes bugs pop up. This work should be prioritized first.

Another part may come from “royal decrees”, tasks and features delegated by higher-ups for completion in the sprint; these should also be avoided, since they are rarely planned for and rarely defined well. Ideally, these should be placed in the Backlog and fleshed out with the aid of a project manager and developer, then added to a later sprint.

For information on how we should conduct Sprint Planning, please see [this document](../supplemental/sprint_planning_checklist.md).

**Backlog Grooming**

Backlog Grooming happens every two weeks. In Backlog Grooming, we do three things: clean up our Backlog, add issues to the Top of the Backlog that we want to work on in the future, and designate design for issues that need it.

Generally, our Backlog will be a bit messy. Issues pop up, and when they do, we make tickets for them that go to the Backlog. There are also tickets for features that are outdated or obsolete. This is especially the case with any legacy application or something inherited from another team or company. We need to go through these, one by one, and determine if they are still relevant, deleting them if they are not.

Next, we review our milestones and add issues to the Top of the Backlog that define completion of these milestones. Requirements gathering will happen here as well. This is also where we add royal decrees, though they should be fleshed out before they are added to the Top of the Backlog.

Finally, for the issues in the Top of the Backlog, we determine which ones need design. Design for stories is done one or more sprints before the story itself, so that development can proceed without having to wait on designs.

**Testing Review (unofficial) (3-4pm Wednesday)**

During testing, documentation is generated which should include discovered bugs, screenshots, steps to reproduce, and any associated error messages. This documentation is reviewed during Testing Review, which should happen before Sprint Planning. During Testing Review, the documentation is reviewed and bugs are discussed. If they are valid, they are turned into Defect tickets in Jira. Critical defects are added to the current sprint to fix ASAP, while other defects are added to the Top of the Backlog.

**Sprint Retrospective**

Sprint Retrospective happens at the end of every sprint. In Sprint Retrospective, we meet as a team to review and reflect on the sprint in a candid manner, following the standard procedure; a plugin in Jira helps facilitate this procedure. First, we write notes in three categories: What went well, What didn’t go well, and Questions. These should be self-explanatory, but the Questions column is something I've added on to allow team members to ask general questions, or pose questions about the work, the team and its processes. Then, we group the notes by topic. There is a Vote step immediately after this but we generally skip that because we place equal value on all posts in the retrospective. Finally, we discuss the posts, addressing them as a group if desired or individually. If there are action items from any of the groups, we create them and assign them to the necessary person. 

**Standup**

Standup happens every morning and is a quick way for us to talk about what we are working on. In it, we follow a standard template. Each person mentions what they worked on yesterday. Then they mention what they are working on today. Finally, they talk about if any item, person, or process is blocking them from working on something. Discussion of said work is kept to a minimum, and if further discussion is needed, it is conducted after Standup. If our work involves working closely with someone from another team, they may be invited to our Standup to mention what they are working on. Standup should be less than ten minutes long.

## Development Pipeline

Our development pipeline defines how we do our work, after we’ve conducted the necessary ceremonies and processes. To view our development pipeline, see [this document](development_pipeline.md).


## Processes

**Requirements Gathering (Milestones - once a quarter, just our; other requirements gathering as needed)**

When a new feature or modification is conceived by a client, a teammate, or a user, steps must be taken to ensure the feature can be developed successfully. A meeting should be set up, formal or informal, that includes the following participants: the client, the project manager, a developer, and a designer. Other participants are optional, though it is important that the four voices are represented: client, project manager, developer, designer. 

All participants will discuss the feature and outline requirements. The client will provide their vision; the project manager will craft the user story and advocate for the developer and designer; the developer will outline rough technical steps, mention scenarios and edge cases, and push back on anything that is not feasible; and the designer will propose visual and experience designs, to which the developer will push back on if they are not feasible. Care must be taken to ensure that all voices are heard and pushback is accepted when provided. When everyone is on the same page, the user story is written and acceptance criteria are defined. These acceptance criteria will be used to develop, test, and verify completion of the story.

**Testing**

After a release has been deployed to our staging machine, our team works through each ticket in the release and tests it. We use the acceptance criteria from the ticket to verify its completion. If a criterion isn’t met, or there is a bug in the implementation, it is logged, along with steps to reproduce the bug. Screenshots are taken to reveal the visual manifestation of the bug. Error statements should also be included, if applicable. These are reviewed during Testing Review and, if they are valid, turned into Defect tickets in Jira. Critical defects are added to the current sprint to fix ASAP, while other defects are added to the Top of the Backlog.

### Issue Types

**Component (Jira/Software-specific)**

A component is not actually an issue type but a Jira/Software object that refers to a component of an application. It is the highest level of object available, so it will allow you to group epics, stories, and tasks within it. Thinking about a web application, one way to describe a component would be as each of the top-level pages available to the user. An example could be the Directory. Within this, we might include epics for Structural Groups, Affinity Groups, and User Profiles.

**Epic**

An Epic is a collection of stories or tasks on a specific topic.

**Story**

A story, shorthand for a user story, is written in the following manner: “As a &lt;user&gt;, I want &lt;a feature&gt; so that &lt;an accomplishment/value proposition&gt;.” Here’s an example: “As a teacher, I want a gradebook so that I can keep track of all my students’ grades.” Stories are written from the user’s perspective because they are the ones that place value in our product; thus, the last part of the story, the accomplishment, can also be defined as the value proposition. Our development on the product should not be based on the features _we_ value, it must be based on what the _user_ values. If we cannot define a user story with a value proposition, then it is not worth writing.

Because stories are more user-centered and high-level, they are easy for a client to conceptualize and write. Stories allow the client to request a feature and not have to worry about the technical requirements. Of course, technical requirements still need to be worked out once the story has been written; for this part, it’s important to have a developer be part of the conversation to ensure the requirements are feasible and doable. These requirements are appended to the user story, either in the Description field, in their own field, or as a comment. Since these requirements are written in collaboration between the client, the developer, and the project manager, they are referred to as Acceptance Criteria: criteria that, once fulfilled, mark the story as complete.

**Task**

A task is more simple than a story; it usually contains just a title and a description of the task. These are usually used to describe something that needs to be done but doesn’t fit cleanly into a current story. A task such as “Add P3P policy”, something technical that needs to be done, may not fit in any user stories.

**Sub-Task**

A story is usually broken up into sub-tasks by a developer, and because of this, these sub-tasks will get pretty technical. Using the user story from above, we can think about how to break it down into sub-tasks. One sub-task might be “Create Grade database model”, while another would be “Create gradebook page”.

**Defect/Bug**

A defect or bug is a software bug encountered by a user or process while using the application. These can take the form of either a literal bug, manifested as an error generated by the application, or as a process that doesn’t function the way it was required to. An example of the first form would be a user encountering a 4xx/5xx HTTP error, or the application generating an error in the form of an alert, notification, or flash message. An example of the second form would be a user attempting to delete an image but having the system hide the image instead of deleting it.

In the description of a defect or bug, the person writing the issue should include the description of the bug, steps to reproduce the bug, the expected behavior/outcome, and the actual behavior/outcome. Providing all of these saves developers a huge amount of time because they are able to quickly reproduce the bug, fix it, and test their code against the expected behavior.

Defects normally are not attached to any other issue type. If possible, they should be prioritized above new development work.

**Sub-Defect**

Much like a sub-task, a sub-defect is a unit of work to be completed for the purpose of fixing the defect or bug. These will usually be written by a developer and be technical as well.

**Technical Debt**

A technical debt describes some amount of functionality that needs to be added or modified on an existing feature for it to work more effectively and efficiently. For example, a developer might write code to enable a user to upload an image to a website. However, as part of processes undertaken by users on the website, such as creating a news article, multiple images are required. The user can still upload images one by one to their article, but eventually, they’ll need to upload multiple images at once to reduce the time needed to author an article. Thus, the technical debt becomes “Refactor image uploads to allow for multiple uploads”.

Like stories, technical debts should be attached to a relevant epic, if applicable.