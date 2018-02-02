# Variables

Variables in Stoplight provide a powerful and intuitive way to allow you to
dynamically set, update, and retrieve information at any step in a Scenario.
Variables can be used in many different ways, however the two primary methods
for using variable data is through:

* __Environments__ - Variables can be persisted in the environment configuration,
  allowing data to be automatically populated depending on the editor's
  environment. See [here](./variables-environment.md) for more information on
  how to use variables in an environment.

* __Contexts__ - Variables can be stored in a scenario "context", allowing for
  test and application state to be persisted between scenario steps. See
  [here](./variables-context.md) for more information on how to use variables in
  a scenario context.

Variables can be used to modify both request and response objects, including
URL's, headers, the request/response body, and more.

***

**Related**

* [Environment Variables](./variables-environment.md)
* [Context Variables](./variables-context.md)
