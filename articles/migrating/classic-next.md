# Stoplight Classic to Stoplight Next Migration Notes

## Platform

|                         |           **Stoplight Classic (v2)**            |                                                                                                         **Stoplight Next (v3)**                                                                                                         |
| :---------------------- | :---------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| **File Types**          |                  RAML and YAML                  |                                                                                                                  YAML                                                                                                                   |
| **Commits**             |               Basic Commit System               |                                                             [Platform backed by Git, all files are Git Repos and have full Git commit support](/platform/projects/git-repo)                                                             |
| **Collaborative Space** |                   Workspaces                    |                                     [Projects](/platform/projects/creating-a-project), [Organizations](/platform/organizations/create-org), and [Teams](/platform/organizations/teams/create-team)                                      |
| **Billing**             |               Individual Billing                | [Individual Billing](/platform/getting-started/billing/plans-overview), [Organization Billing](/platform/getting-started/billing/organization-plan-overview), and [Fair Billing Policy](/platform/getting-started/billing/fair-billing) |
| **Swagger Extensions**  |                  Not supported                  |                                                                                                                Supported                                                                                                                |
| **Change History**      |              Basic Commit History               |                                                                               [Full Commit History Backed by Git](/platform/editor-basics/change-history)                                                                               |
| **Project Visibility**  |                Private Projects                 |                                                                             [Private and Public Organizations and Projects](/platform/projects/visibility)                                                                              |
| **Guest Role**          | Guests (read-only) count towards your team size |                                                               [50 Guest limit that doesn't count towards your team size](/platform/getting-started/billing/fair-billing)                                                                |
| **Ref Builder**         |                  Not supported                  |                                                                                       [Supported](/documentation/referencing-other-data-sources)                                                                                        |
| **Access Tokens**       |                  Not supported                  |                                                                                                                Supported                                                                                                                |
| **Code View**           |                  Not supported                  |                                                                                       [Supported](/platform/editor-basics/read-design-code-view)                                                                                        |

## Modeling

|                          | **Stoplight Classic (v2)** |                                     **Stoplight Next (v3)**                                     |
| :----------------------- | :------------------------: | :---------------------------------------------------------------------------------------------: |
| **Shared Specification** |           Traits           | [Shared Models and Parameters](/modeling/modeling-with-openapi/shared-parameters-and-responses) |
| **Grouping**             |          Grouping          |                [Hubs Ref Builder](/documentation/referencing-other-data-sources)                |
| **Documentation Design** |          Modeling          |                               [Hub](/documentation/introduction)                                |
| **API Discovery**        |         Supported          |                                           Coming Soon                                           |
| **Bulk Editing**         |         Supported          |                [Code View Editor](/platform/editor-basics/read-design-code-view)                |

## Hubs

|                            | **Stoplight Classic (v2)** |                                                     **Stoplight Next (v3)**                                                      |
| :------------------------- | :------------------------: | :------------------------------------------------------------------------------------------------------------------------------: |
| **Documentation Produced** |       API Reference        |                             API Reference, Supplementary Documentation, and Auxillary Documentation                              |
| **Linking**                |            SRN             |                                                             Markdown                                                             |
| **Routes**                 |            Slug            |                                        [Markdown](/documentation/getting-started/routing)                                        |
| **Hiding Models**          |         Supported          |                                                           Coming Soon                                                            |
| **Authentication**         |  Basic Auth and OAuth 2.0  | [Basic Auth, Auth0, OAuth 2.0, and SAML with multiple security scheme support](/modeling/modeling-with-openapi/security-schemes) |
| **Workflow**               | Creation through Modeling  |                               [Standalone Documentation Tool](/documentation/introduction) (Hubs)                                |
| **Custom Domain**          |       Email Support        |                                                            Automated                                                             |

## Prism

|                        |                      **Stoplight Classic (v2)**                      |                   **Stoplight Next (v3)**                    |
| :--------------------- | :------------------------------------------------------------------: | :----------------------------------------------------------: |
| **HTTP Requests**      |                          Logs HTTP Requests                          |                         Coming Soon                          |
| **Prism Instances**    |       Every version supported by Mock Server and Proxy Server        | [Unlimited amount of Prism Instances](/mocking/introduction) |
| **Javascript Runtime** |     [API](https://help.stoplight.io/prism/runtime-reference/api)     |              [API](/mocking/javascript-runtime)              |
| **Prism Command Line** | [Commands](https://help.stoplight.io/prism/getting-started/commands) |                       Commands Changed                       |

## Scenarios

|             | **Stoplight Classic (v2)** |                **Stoplight Next (v3)**                |
| :---------- | :------------------------: | :---------------------------------------------------: |
| **Testing** |       Not Available        | [Integrated into the platform](/testing/introduction) |
