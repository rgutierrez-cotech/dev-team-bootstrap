# Sprint Planning checklist

This is a rough outline of one of our sprint planning meetings.

1. Create sprint if needed
2. Determine velocity. We will use this number as the maximum number of story points we can assign during this sprint.
3. Ask questions to determine sprint workload
    1. What do we need to carry over from last sprint? (prioritize bugs)
    2. Royal Decrees - what stories/tasks do our clients/executives/shareholders want us to work on?
    3. What can we add to this sprint?
        1. Bugs (defects)
        2. Stories that already have design and acceptance criteria, or stories that don't need design
        3. Technical debts
    4. What can we start designing for in the next sprint or upcoming sprints?
4. Assign Estimate (story points or equivalent measurement of work) to all issues in sprint by conducting Planning Poker
    1. If you'd like to track testing effort in your Jira, you can try this: for stories, assign a Test ticket (this is a custom ticket type I created), copy over the acceptance criteria, and set the story points to 40% of the story’s estimate, rounded. This Test ticket will be assigned to the code reviewer
5. Add up Estimate from Stories, Defects, and Design Specifications (Design Specification is another custom ticket I created to track our design work)
6. If total is greater than our velocity, remove some issues from the sprint, starting with debts, then stories (excluding royal decrees)
7. Assign all issues to a person
8. If your tickets have a default status other than To Do: bulk edit all issues from the sprint and set Status to To Do
9. After sprint has been planned, create a Release in Jira, bumping the minor release number by 1. If this is not a minor release, bump the appropriate number by 1.
10. Bulk edit all issues from the sprint and set Fix Version to the new Release