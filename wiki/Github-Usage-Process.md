
The purpose of this document is to explain the proper use of Github and task management while using the eos.io repository.

## Goals

1. By using the In Progress tag, anyone should be able to see all work that is currently underway.  This should also exclude any issues **not** being worked on.
2. Tying tasks to issues makes sure that:
    - We are not working on the same issue at the same time
    - Dan is able to track progress and performance

## Process Summary

1. All commits must be associated with an existing issue.
2. When working on an issue, add the "In Progress" tag
3. Only have a max of one "In Progress" tag on an issue at any time
4. When not actively working on an issue, remove the "In Progress" tag
5. When opening pull requests, reference the issue in the description of the pull request
6. Check in your work daily
7. If you see improper usage, call it out! The team will be strongest when everyone is working the process together

### 1. All commits must be associated with an existing issue.

Part of GitHub's functionality is an issue tracker called "Issues," which can be used with every repository. It can be accessed via the repositories issues tab

If there is no issue for the planned unit of work, the first step is to create an issue.

Every issue should contain:

1. A short and descriptive bug report title
2. In the body of the issue: A summary of the issue along with reproduction steps if suitable. Further information such as development environment, stack traces or error messages should be included for extra clarification, if possible.
3. A set of tags which correspond to the issue. This can be either a tag that groups the issue with related issues (such as the "documentation" tag) or expresses severity ("PRIORITY" tag).

### 2. When working on an issue, add the "In Progress" tag

In order to avoid collisions when two people work on the same issue, every developer needs to set the "In Progress" tag to the issue they plan to work on BEFORE the work actually starts. This step is furthermore of utmost importance, as it provides Dan with a way to track progress and reassign work in case issues of higher importance need to be fixed.

### 3. Only have a max of one "In Progress" tag on an issue at any time

It is important, that every developer needs to have only one "In Progress" tag set at any time. This is to avoid accumulating a number of issues that are all half finished and therefore hindering other developers from picking them up, which in effect blocks the issue from being fixed.

### 4. When not actively working on an issue, remove the "In Progress" tag

As mentioned in the above paragraph, in order to avoid blocking an issue to be fixed by other developers, the "In Progress" tag needs to be removed as soon as the developer moves onto a different issue.

However it is necessary to add an explanation to the issue itself which explains, what work has been done on the issue, what subtasks have been finished and why the developer moved onto a different issue instead of finishing the task completely.

Note: In case there was a block that made it impossible to fix the issue in the first time, a reference to the blocking issue has to be included in the explanation so it can be revisited once the blocking issue has been resolved and closed. Additionally there is a "blocked" tag which needs to be set.
<br/><br/>
### 5. When opening pull requests, reference the issue in the description of the pull request

After fixing an issue, open a pull request, with a proper explanation.

The explanation includes:

1. A reference to the github issue; There should always be an issue before a unit of work is done. If there is no issue, it needs to be created as the first step, followed by the above described work flow.
2. A description of the fix: How has the issue been fixed? What is the expected outcome after closing of the issue?
3. In case the the fix has changed any functionality that either requires additional documentation to be added or existing documentation to be changed, it is HIGHLY recommended that the documentation work is part of the pull request. In case this is not done, the description needs to include keynotes on what documentation is either missing or which documentation needs to be changed.

### 6. Check in your work daily

At the end of the work day, submit your changes. In case an issue has been completely fixed, follow the above described process. When not finished with a task, submit the changes to your feature branch and explain the progress in the submission.

Note: This step is very important, since it enables Dan to track progress, plan future development and coordinate further task assignments.

### 7. If you see improper usage, call it out! The team will be strongest when everyone is working the process together

Following the rules set above, are about streamlining the development process. They are essential in fulfilling the goals mention at the top of this document. This is even more important since the team is working in a distributed fashion with limited communication between the different team members.
