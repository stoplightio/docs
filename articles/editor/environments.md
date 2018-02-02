# Environments

<!--(FIXME - SHOW CLICKING BETWEEN DIFFERENT ENVIRONMENTS)-->

The Stoplight editor includes an embedded configuration system that can be used
to auto-populate environment information and other variables (hostnames, ports,
passwords, etc.) utilized by specifications, scenarios, or collections. To
display the current editor environment variables, click the icon on the top
right of the Stoplight editor as shown in the image above.

<!--(FIXME - SHOW SCREENSHOT OF THE ENVIRONMENTS WINDOW)-->

For more information on environment variables and how they can be used, please
see [here](../testing/variables-environment.md).

## Private Variables

Private Variables are variables that are _only_ stored locally on your system
and are never sent to Stoplight or the rest of your team. Private variables
should be reserved for secrets specific to you, such as user-specific passwords,
API keys, and other pieces of sensitive data.

> Since private variables are only stored on your computer, make sure they are
  backed up in a secure location

## Resolved Variables

Resolved Variables shows a read-only view of the variables that are currently
exposed to your editor, based on:

* Your current environment
* Your private variables

These variables (excluding your private variables) are stored in the
`.stoplight` file of your project (under "Config" in the File Explorer). 

The Resolved Variables displayed in the editor will change depending on your
current environment. To update the default or environment-specific variables
stored in Stoplight, click the "Manage Environments" button under the
configuration window.

<!--(FIXME - SHOW GIF OF CLICKING MANAGE ENVIRONMENTS BUTTON)-->

For more information on updating and customizing environment variables, please
see [here](./editor-configuration.md#environments).

***

**Results**

* [Using Environment Variables](../testing/variables-environment.md)
* [Configuration with the `.stoplight.yml` File](./editor-configuration.md#environments)
