# Environments

An environment is simply a container for data, represented as a list of key-value pairs (behind the scenes, this is a JSON object). Every Stoplight project has one or more environments associated with it. The data stored in an environment can be used in many places within the Stoplight editor.

![How to open the Environments window](https://github.com/stoplightio/docs/blob/develop/assets/images/environments.png?raw=true)

Environments, and their default data, are defined in the [Stoplight configuration file](/platform/editor-basics/editor-configuration).

* **Do** create an environment for each development environment associated with the project. For example, `development`, `staging`, and `production`.
* **Don't** create environments for individual users. Instead, use private variables (below) to customize existing environments.
* **Do** use environment default data to store shared information like hostnames, ports, passwords, etc.
* **Don't** use environments to store fixture/seed/temporary data.

![The Environments Window](https://github.com/stoplightio/docs/blob/develop/assets/images/environments2.png?raw=true)

For more information on environment variables and how they can be used during API testing, please
see [here](/testing/using-variables/environment).

## Private Variables

Private Variables are _only_ stored locally on your system,
and are never sent to Stoplight or the rest of your team. Private variables
should be reserved for secrets specific to you, such as user-specific passwords,
API keys, and other pieces of sensitive and/or individually specific data.

Edit private variables by clicking on the environment button in the top right of the Stoplight editor.

> Since private variables are only stored on your computer, make sure they are
> backed up in a secure location.

## Resolved Variables

Resolved Variables shows a read-only view of the variables that are currently
exposed to your editor. They are based on:

* The currently selected (active) environment
* The active environment's default variables, as defined in the stoplight configuration file
* The active environment's private variables, as defined by you

Private variables are merged over default variables that share the same name. This makes it easy
for individual team members to customize and extend environments without affecting the rest of the team.

For more information on updating and customizing environment variables, please
see [here](/platform/editor-basics/editor-configuration).

---

**Related Articles**

* [Working with Files](/platform/editor-basics/working-with-files)
* [Change History](/platform/editor-basics/change-history)
* [Editor Configuration](/platform/editor-basics/editor-configuration)
* [File Validation](/platform/editor-basics/file-validation)
