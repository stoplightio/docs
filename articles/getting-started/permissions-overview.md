# Permissions & Governance Overview 

## Organizations 

| **Organization Actions**        | **Guest** | **Member** | **Administrator** | **Owner** |
|---------------------------------|:-----------:|:------------:|:-------------------:|:-----------:|
| Read Public Projects            |     X     |      X     |         X         |     X     |
| View Organization Collaborators |           |      X     |         X         |     X     |
| View Organization Teams         |           |      X     |         X         |     X     |
| Create Projects                 |           |      X     |         X         |     X     |
| Read Private Projects           |           |      X     |         X         |     X     |
| Write Projects                  |           |            |         X         |     X     |
| Manage Collaborators            |           |            |         X         |     X     |
| Manage Teams                    |           |            |         X         |     X     |
| Manage Organization Settings    |           |            |                   |     X     |
| Manage Organization Billing     |           |            |                   |     X     |
| Delete Organization             |           |            |                   |     X     |

## Teams 

|      **Team Actions**     | **Member** | **Administrator** | **Owner** |
|-------------------------|:------------:|:-------------------:|:-----------:|
| View Team Collaborators   | X          | X                 | X         |
| Add Team to Projects      | X          | X                 | X         |
| Manage Team Collaborators |            | X                 | X         |
| Manage Team Settings      |            | X                 | X         |
| Delete Team               |            |                   | X         |

## Projects 

| **Project Actions**          | **Read** | **Write** | **Administrator** |
|------------------------------|:--------:|:---------:|:-----------------:|
| Read Project                 | X        | X         | X                 |
| Write Project                |          | X         | X                 |
| Manage Project Collaborators |          |           | X                 |
| Delete Project               |          |           | X                 |
