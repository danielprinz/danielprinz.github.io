---
title: Continous Integration with Gitlab and Gitlab CI
gitlab: gitlab, gitlab-ci, gitlab-runner, gitlab-tags
---

For **fast and high quality development of software** a continous integration workflow is essential. It is import to get early feedback if the integration with other components works.
A simplified circle looks like this:  
![continous integration](/img/2018-01-20-continous_integration.png){:width="350px"}
Source: [continuous-integration-for-salesforce-lightning-development](https://medium.com/salesforce-developers/continuous-integration-for-salesforce-lightning-development-a59adf1a21be)

## Development Workflow
In the last few weeks I did set up a **CI environment with GitLab** for the project my company. For the sake of keeping it simple I tried to achieve most the cycle with one tool.
1. Writing an issue in Gitlab.
2. Adding a checklist for all tasks.
3. Start working on the issue, create a feature branch and update it during development.
4. When the feature is finished create a merge request.  
5. After the branch is merged, the ticket can be closed.   

## CI-Pipeline
Every time something is pushed to a git-branch the Gitlab CI takes care that all tests are executed and gives feedback when something fails. There is a big amount of different integrations that can be used to get a notification for the broken build. Because it is cool I used Slack for it :D.  
A whole pipeline for Gitlab can be defined in a single *gitlab-ci.yml* file.

A simplified  *gitlab-ci.yml* file for a java-maven project would look like this:
{% gist danielprinz/6d8d34695395bee2ee712189bd65cc55 %}

There a many official templates available here: [Gitlab-CI-Templates](https://gitlab.com/gitlab-org/gitlab-ci-yml)

## Gitlab-Runners
Every job in the pipeline is running on a Gitlab-Runner. There are different kinds of Gitlab-Runners.  
* *Shared Runners*  are globally available for every project.  
* *Dedicated Runners* are only processing jobs of a specific project.  
  
Adding and enabling *dedicated runners* for every project was very cumbersome and took some time. It is also not that clealy visible which runner is enabled for which project. A better way to manage the different Gitlab-Runners is through Gitlab-Tags.
### Gitlab Tags
Gitlab tags are very handy for defining **which runner should process a specific build job.** So for example there are two different *shared runners*.  
  
One has maven installed and can build maven projects. The other has docker installed and can build docker images.  
* first runner gets the tag **maven**  
* second runner gets the tag **docker**  

The only missing step is now to add the tag **maven** to the **gitlab-ci.yml build job** and the tag **docker** to the **gitlab-ci.yml deploy job**.  This concept makes scaling very easy. If you have many java projects, just add more Gitlab-runners with maven installed and give them the correct tag.
## Optional: Deployment with Docker
Again to keep it simple and make deployment easier, the project artifacts are added to a docker container. This docker container is pushed to the docker registry that is provided by Gitlab. Accessing the images is now very easy, because for every project there is a section called *Registry*.

## Conclusion
My experience with Gitlab is quite good. It removes the fact to change between many tools. That helps the system administrator and the users. :)