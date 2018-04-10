# Git Repositories
 
## What 
* The Stoplight Platform is built on top of git
* All Stoplight projects are a git repository
* You can use Access Tokens to access the Stoplight API, authenticate Prism in a continuous integration environment, and access the underlying git repositories for projects
* You can make this part of your git workflow, add it to scripts, or your CI/CD process

## How

Under the Settings section in your Stoplight account, find the “Access Tokens” section. 

[image]

You will create an token to access projects that your Stoplight account has proper permissions for. These permissions match the ones in the Stoplight UI. 

If you have write access to a project, you will be able to:
* Pull projects via git
* Commit to projects via git
* Push changes to projects via git

If you have read access to a project, you will be able to:
* Pull your project via git

You can name the token whatever you want. Once you have created an Access Token, copy it and only store it in safe location. Once you close the window, you will not see it again.

We recommend to store it as an environmental variable. For example, on Mac/Linux:

`export STOPLIGHT_TOKEN="1234567890"`

You can then `git clone` the repo: 

`git clone https://{stoplight-username}:$STOPLIGHT_TOKEN@git.stoplight.io/{username}/{project-name}.git`

For example: 

`git clone https://taylor:$STOPLIGHT_TOKEN@git.stoplight.io/taylor/test-new.git`

If it is a project from an organization and not a personal project, replace `username` with `organization-name`. 

Now you can make changes to your files, commit, and push to your master branch. These changes will then be seen in the Stoplight UI as well as the "History of Changes." 

Remember: Only changes on the master branch will be seen in the UI at this time. 

    
---
**Related Articles**
- [Change a Project Member's Role](/platform/projects/change-a-members-role)
- [Make Your Project Private/Public](/platform/projects/visibility)
- [Invite People to Organization](/platform/organizations/invite-people)
- [Add People to a Team](/platform/organizations/teams/add-people)
