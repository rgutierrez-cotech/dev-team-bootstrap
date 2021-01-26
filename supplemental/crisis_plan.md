## Crisis Plan

This is an attempt to outline an informal guide for current and future developers to aid them in solving various crises that may arise within our applications. These can include: bugs (within our code, within a library, etc.), hardware failures (container/vm crashes, cloud service outages), and data corruption (usually associated with a bug but could be from a database failure), among other things.

**Restore service to users**

The top priority in any crisis is to restore normal service to users of the application. This can mean rolling back the deployed code to a previous, working version, or shutting down/rolling back the particular microservice that is causing the error. In the case of data corruption, this may mean rolling back the database to a previous, working version, though that effectively means “erasing” any work done by users within the application since the previous database backup. Therefore, try to divert users away from the corrupted data if possible, by using the above methods, before considering this method.

If done correctly, service should be restored while keeping the affected instance/container/vm live and addressable only by our developers. We will need access to determine the cause of the problem shortly.

It’s worth mentioning the **nuclear option**, which is to **completely shut down the application**. This should be saved as a last resort and/or used in extreme circumstances, such as an active hacking attempt.

**Identify the likely cause of the problem**

Review all relevant logs from the affected instance to determine the likely cause of the problem. Connect to the affected instance and try to reproduce the issue. We may not be able to determine the _exact_ cause but we will learn enough to put us down the right track to solving. Knowing what services are affected and how they are affected is a great starting point.

**Prepare and release a public statement**

Optionally, after restoring service to users and identifying a likely cause, we should release a public statement via email blast, our website, and/or social media addressing the bug and anticipated rollback/outage. If the bug was disruptive but only affected a single system, and we were able to correct with a rollback, this might not be necessary. If the bug was majorly disruptive, affecting multiple systems, and/or rendering the application unusable, releasing a public statement is a good idea. It is likely numerous users experienced the bug and will be communicating about it with us, their colleagues, even on social media. This can turn other users away from the application and can reduce our credibility if the issue is not resolved quickly.

The statement should express our apologies and mention our active efforts at resolving the issue. It can include as much detail regarding the issue as desired, though a brief summary is often good enough. No summary at all is usually okay as well. When the bug is fixed, another statement should be released to share the news and thank everyone for their patience. This should be released via the same channels as the previous statement.

Here is an example of a statement:


```
This morning, a bug within our new PDSA feature caused a service outage for many of our NILS users. We have disabled the feature and are actively working on a solution. We apologize for the inconvenience!
```


And once the issue is fixed, we can release another statement:


```
Our team has fixed the bug and are reporting no further issues. Thank you for your patience!
```


**Gather information**

This is a continuation of “identify the problem”. More exploration can be done once service is restored and an optional statement has been released.

Check _all_ logs for information related to the problem. This includes (and is not limited to): access and error logs (might be the same things depending on the application), service-specific logs (database logs, routing logs, email service logs), and any custom log files. Form a complete picture of the problem and determine the _exact cause_.

Determine when the issue needs to be fixed. This is almost always ASAP but there may be other factors at play, such as users needing the affected service for an upcoming event or demo. In this case, there is a “hard deadline” by which the issue needs to be fixed.

**Form a “quick and dirty” solution**

Determine what needs to be done to fix the issue ASAP, without regard to code quality, development roadmaps, and standard procedure. This is our “quick and dirty” solution, which is never ideal, but it is our _backup_ in case we fail to implement the real solution in time for our hard deadline. Estimate the time to completion and keep this information handy.

**Form a “real” solution**

How will we correct the problem for real? Our real solution should follow our normal bug fixing and development procedures. Task it out, estimate the time to completion, and get to work. Depending on the time needed and the severity of the issue, development time outside of work hours may be necessary. No one ever wants to do this, and encouragement, along with pizza and frequent breaks, can make it more bearable, but it can be avoided by implementing the QDS (quick and dirty solution) if we run out of time. Which leads us into the next step…

**Monitor time spent**

Remember how long it would take to implement our QDS? Say we need more time for our real solution, more time than we have. If our remaining time is equal to the time needed for the QDS, stop development on the real solution and do the QDS. Once the QDS is complete, write the necessary tickets in Jira detailing the technical debt we just accumulated.

If we can make it in time, finish the real solution and deploy.
