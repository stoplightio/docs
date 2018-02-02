# Using Environment Variables

<!--(FIXME - SHOW CLICKING THROUGH ENVIRONMENTS IN UI)-->

> If you have not already done so, we recommend reviewing the
[Environments](../editor/environments.md) article before continuing.

Environment variables in Stoplight allow you to dynamically retrieve information
in a scenario using the editor's [environment
configuration](../editor/editor-configuration.md). This makes it possible to
switch between different environments with ease, having variables automatically
populate based on the current environment.

## Setting Environment Variables

### With the Editor Configuration

For information on setting environment variables, please review the [environment
configuration](../editor/editor-configuration.md) article.

### With Scripting

Scripting allows you to use more complicated logic in a scenario step. Scripts
are executed either before or after a step request finishes. Scripts are plain
Javascript and give you direct access to the scenario environment through the
global `$$.env` object.

To add variables to the environment, use the following syntax:

```javascript
// store the step output body's 'hostname' object in the environment
$$.env.set('hostname', output.body.get('hostname'));
```

Where the `$$.env.set(x, y)` function adds the data referenced in the second
argument (`y`) to the environment under the string value of the first argument
(`x`).

> Environment variables set via script are only added to the user's private
  variables, and are not sent to Stoplight. See the [Environment
  section](../editor/environments.md) for more information.

## Referencing Environment Variables

<!--(FIXME - SHOW USING A VARIABLE IN A SCENARIO STEP)-->

To reference an environment variable in a scenario, use the following syntax:

```
{$$.env.myVariable}
```

Where:

* `{...}` - Braces signify that this is a variable reference. See the [variables
  overview](./variables-overview.md) section for more information on how
  variables are used.
* `$$` - The "double dollar sign" syntax is a reference to the scenario's global
  scope.
* `env` - Every scenario has a global `env` property that signifies this being a
  reference to the editor's environment.
* `myVariable` - This is the variable being referenced, which comes from the
  project's `.stoplight.yml` file. Substitute your own variable name when using
  this in a scenario.

When the scenario or step is run, any environment variable references will
automatically be populated based on the editor's current environment.

### In Scripts

Similar to the example above, when referencing an environment variable in a step
script, use the following syntax:

```javascript
$$.env.get('myVariable');
```

Where the braces (`{}`) are absent, and we are using the `get()` method for
retrieving the environment variable under the `myVariable` key.

***

**Related**

* [Environment Overview](../editor/environments.md)
* [Environment Configuration](../editor/editor-configuration.md)
* [Variables Overview](./variables-overview.md)
* [Context Variables](./variables-context.md)
