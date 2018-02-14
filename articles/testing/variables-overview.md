# Variables Overview

Variables in Stoplight provide a powerful and intuitive way to dynamically set, 
update, and retrieve information at any step in a Scenario.

Variables are stored in an [environment](../editor/environments.md). You can define one or more environments,
each with their own variables. This makes it easy to quickly swap out sets of 
variables during testing.

There are a variety of circumstances where you might consider using variables instead of hardcoding the value, for example:

- __hostnames__: Instead of hard-coding a particular server location, use a variable
so that the host can quickly be changed to test multiple server locations (development versus production, for example).
- __api keys__
- __usernames and passwords__
- __ports__
- __path parameters__: Instead of defining a request `GET /users/123`, you can define a request `GET /users/{$$.ctx.userId}`.

There are two scopes for variables, which affect how and when they can be used.

* __Environment Variables__ - Environment variables are scoped to the project, and are shared amongst all steps in your test run. They are persisted between test runs, and are great for data that does not change often (hostnames, ports, etc). See [here](./variables-environment.md) for more information on how to use environment variables.

* __Context Variables__ - Context variables are scoped to the scenario, and are reset on every test run. They are useful to persist test and application state between scenario steps. Context variables are great for temporary information that is only relevant to the current test run. For example, you might store a newly created `userId` returned in your first step, to be used in the second step. This `userId` changes on every test run, which makes it a good context variable candidate. See [here](./variables-context.md) for more information on how to use context variables.

***

**Related**

* [Environment Variables](./variables-environment.md)
* [Context Variables](./variables-context.md)
