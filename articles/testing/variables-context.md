# Using Context Variables

<!--(FIXME - SHOW WRITING VARIABLE TO CONTEXT IN STEP)-->

Context variables allow you to dynamically store and communicate
data between various steps in a scenario. Stoplight stores data in the scenarios "context", which makes it possible to initialize and store data in one step. This allows data to be used again in subsequent steps. 


Data stored in the context is _not_ saved once a test has completed. Therefore, it is
important to only store useful temporary data within the current test or
scenario execution. At the start of a test run, the scenario context is emptied.
Good examples of data to store in a context would be things like ID's,
usernames, and randomly generated tokens.

## Setting Context Variables

### With Captures

<!--(FIXME - SHOW USING THE CAPTURE MENU IN A SCENARIO STEP)-->

By using a "capture" in a scenario step, data can be saved to the current
context by referencing either the step output, the scenario response, the
environment, or the step context.

<!-- theme: info --> 
>Multiple captures can be applied to the same step.

### With Scripting

<!--(FIXME - SHOW SCREENSHOT OF SCRIPT IN STEP)-->

Scripting allows you to use more complicated logic in a scenario step. Scripts
are executed either before or after a step request finishes. Scripts are plain
Javascript and give you direct access to the scenario context through the global
`$.ctx` object.

To add variables to the scenario context, use the following syntax:

```javascript
// store the step output body's 'apiKey' object in the context
$.ctx.set('apiKey', output.body.get('apiKey'));
```

Where the `$.ctx.set(x, y)` function adds the data referenced in the second
argument (`y`) to the context under the string value of the first argument
(`x`). 

Here is another example:

```javascript
myVariable = "hello";
$.ctx.set('myVariable', myVariable);
```

## Referencing Context Variables

<!--(FIXME - SHOW USING A CONTEXT VARIABLE IN A SCENARIO STEP)-->

To reference a context variable in a scenario, use the following syntax:

```
{$.ctx.myVariable}
```

Where:

* `{...}` - Braces signify that this is a variable reference. See the [variables
  overview](./variables-overview.md) section for more information on how
  variables are used.
* `$` - The "single dollar sign" syntax is a reference to the current scenario's
  runtime scope.
* `ctx` - Every scenario step has a `ctx` property that allows access to the
  runtime context (where variables can be stored for later use).
* `myVariable` - This is the variable being referenced within the context.

When the scenario or step is run, any context variable references will
automatically be populated based on the contents of the scenario context at
runtime.

### In Scripts

Similar to the example above, when referencing a context variable in a step
script, use the following syntax:

```javascript
$.ctx.get('myVariable');
```

Where the braces (`{}`) are absent, and we are using the `get()` method for
retrieving the context variable under the `myVariable` key.

***

**Related**

* [Environment Overview](../editor/environments.md)
* [Environment Configuration](../editor/editor-configuration.md)
* [Variables Overview](./variables-overview.md)
* [Context Variables](./variables-context.md)
