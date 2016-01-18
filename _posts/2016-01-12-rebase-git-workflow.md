# Rebase Git Workflow

There are different kinds of workflows available as a developer when working on teams. You can read more about them [here](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow). 

I will give a brief overview of working on a team using the rebase git workflow.

##### The Problem
---
Working on the same code base with a team can be a difficult process. Imagine trying to cook in the same kitchen while doing similar roles and getting a delicious dish at the end. As much as you try to assign people different parts of the code base, there is going to be overlap. And overlap could be editing the same file on the same line. Or deleting a file that you modified. Now you have to decide which code you want to keep and which you want to remove. 

![code conflict image](https://code.visualstudio.com/Content/images/versioncontrol_merge.png)

Above is an image someone shared online. As you can see, the developer now has to decide between keeping the code between Head, or the one between master. 
```
<<<<<<< HEAD
your changes/code
=======
your team memebers changes/code
>>>>>>> branch-a
```
You have to decide what makes sense for the to be new code base. 

##### The Solution
---
<iframe src="https://docs.google.com/presentation/d/1WHslJlqyHUDEsWaWnQ-LIG2kLX37kIdAqpA2dEyRAHg/embed?start=false&loop=false&delayms=3000" frameborder="0" width="520" height="350" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>


