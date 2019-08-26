# Using Environment Variables

> If you have not already done so, we recommend reviewing the
> [Environments](/platform/editor-basics/environments) article before continuing.

Environment variables in Stoplight allow you to dynamically retrieve information
in a scenario from the active environment. This makes it possible to
switch between different environments with ease, having variables automatically
populate based on the current environment.

![](https://s3.amazonaws.com/user-content.stoplight.io/1564/1521753220632)

## Setting Environment Variables

### With the Editor Configuration

For information on managing project environments, please review the [environment](/platform/editor-basics/editor-configuration) article.

### With Captures

Captures make it easy to "capture" values from your step request or result, and save them back to an environment variable for later use. Simply switch to the `captures` tab in the scenario step, and choose $$.env as the target property.

Say you have a scenario step that sends an HTTP request to authenticate a new user. The response from that request includes an apiKey that you want to use for other requests. You can easily save that apiKey to an environment variable, for later re-use, by adding a capture in the form `$$.env.apiKey = output.body.apiKey`. After running the step, check your current environment variables and note the newly added apiKey!

> Environment variables set via captures are only added to the user's private
> variables, and are not sent to Stoplight. See the [Environment
> section](/platform/editor-basics/environments) for more information.

### With Scripting

Scripting allows you to use more complicated logic in a scenario step. Scripts
are executed either before or after a step finishes. Scripts are plain
Javascript and give you direct access to the scenario environment through a
global `$$.env` object.

To add variables to the environment, use the following syntax:

```javascript
// store the step output (response) body's 'username' property in the environment
$$.env.set('username', output.body.get('username'));
```

Where the `$$.env.set(x, y)` function adds the data referenced in the second
argument (`y`) to the environment under the string value of the first argument
(`x`).

> Environment variables set via script are only added to the user's private
> variables, and are not sent to Stoplight. See the [Environment
> section](/platform/editor-basics/environments) for more information.

## Using Environment Variables

Use an environment variable in a scenario with the following syntax:

```
{$$.env.myVariable}
```

Where:

* `{...}` - Braces signify that this is a variable.
* `$$` - The "double dollar sign" syntax is a reference to the global
  scope.
* `env` - The `env` property holds the active environment's data.
* `myVariable` - This is the variable being referenced, which comes from the
  active environment's resolved variables. Substitute your own variable name when using
  this in your scenarios.

When the scenario or step is run, any environment variables will
automatically be populated based on the editor's active environment.

### In Scripts

Similar to the example above, when referencing an environment variable in a step
script, use the following syntax:

```javascript
$$.env.get('myVariable');
```

Where the braces (`{}`) are absent, and we are using the `get()` method for
retrieving the environment variable under the `myVariable` key.

---

**Related Articles**

* [Editor Configuration](/platform/editor-basics/editor-configuration)
* [Environments](/platform/editor-basics/environments)
* [Using Variables Overview](/testing/using-variables/overview)
* [$.ctx(Context)](/testing/using-variables/context)
