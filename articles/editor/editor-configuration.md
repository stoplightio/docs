# Configuration with the `.stoplight.yml` File

This document describes the usage of `.stoplight.yml`, the file that is used by the Stoplight editor to manage its configuration.

It is placed in the root of your project and allows you to configure editor settings and environments that will apply to **all** users of the project. This allows you to share commonly-used settings between members of your team directly.

You can make changes to the `.stoplight.yml` file by opening it:

![Editor Configuration Location](https://github.com/stoplightio/docs/blob/develop/assets/images/editor-configuration.png?raw=true)

### Editor Configuration

- **defaultFile**: The `defaultFile` setting allows you to control which file is displayed to read-only users when they navigate to the project. This can be useful to show them a particular markdown or hub on first load.

### Environments

![Environments](https://github.com/stoplightio/docs/blob/develop/assets/images/editor-configuration2.png?raw=true)

Environments make it easy to auto-populate variables (hostnames, ports, passwords, etc.) used by specifications and scenarios. Read more about them [here](/testing/using-variables/environment).

The environments and variables defined in the `.stoplight.yml` are shared amongst all users, which makes this a good place to define common or shared variables, such as the url host for a particular API + environment. 

There are three environments included with a new project:

* __Default__ - The __Default__ environment is used by the Stoplight editor when first logging in and if no other environment has been selected. This is commonly used for variables needed for development and prototyping.
* __Staging__ - The __Staging__ environment is automatically created for the storing of"staging" or "pre-production" variables and settings.
* __Production__ - The __Production__ environment is automatically created for the storing of production variables and settings.

These environments can be customized by editing the `environments` key of the `.stoplight.yml` file. To add a new environment, simply add a new key to the `environments` property, and set the value to an empty object or an object with default variables to share amongst your team.

***

**Related Articles**

* [Testing Environment Variables](/testing/using-variables/environment)
