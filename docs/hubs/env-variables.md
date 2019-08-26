# Env Variables for Documentation 

![Env Variables](https://github.com/stoplightio/docs/blob/develop/assets/imagesv2/env-variables.png?raw=true)

## What 

You can input default values for env variables within your documentation to assist users in testing endpoints or to make documentation specific to the user. You can input default values for markdown, security schemes, API hosts, query parameters, headers, and much more. You can also further modify what kinds of default values you can push to your documentation with JavaScript and modified URLs.

## How 

### Using $$.env in a Hub, API, or Markdown File

Use the syntax `{{$$.env.variableName}}` anywhere you want some value to be replaced. For example, as a default value for a header parameter or in your API’s description field or even in a markdown file.

### Setting default values for $$.env during the build process

You can optionally have these $$.env variables replaced during the build process. This is useful if you are publishing the same API or Hub for different customers and need to change specific things (like an API Host) for each one.

1. Select the **project** you wish to modify 
2. Select the **publishing icon** in the far left-hand menu 
3. Select the **domain** you want you to input default env values for
4. Under Advanced, select **Env Variables** 
5. Input the env variables you want to add default values for 

> Tip: Copy and paste env variable data from **Environments** to save time 

### Setting $$.env using your Hub’s URL

If you would like to replace a variable after a Hub has been built, you could do so by adding them to your browser query. A use-case for this would be if you have a customer that has a specific API, you could send them to your docs with the apikey in the query.

1. Add ```?variable to modify=default value``` to the end of the URL of published documentation 

> Example: ```https://docs.stoplight.io?username=Chris&apikey=234```

For the visitor of your Hub, this will replace any occurrences of `{{$$.env.username}}` with the text ”Chris” and `{{$$.env.apikey}}` with 234.

### Setting $$.env using JavaScript 

For more advanced use-cases, you can update the variables programmatically! For example, if you are using Auth0, you could get some information from their API after your user logs in. You can then use javascript to update any variables that are specific to them such as `{{$$.env.username}}` or {{$$.env.apikey}}`.

1. Select the **project** you wish to modify 
2. Select the **publishing icon** in the far left-hand menu 
3. Select the **domain** you want you to input default env values for
4. Under Advanced, select **JavaScript**
5. Input the script ```__SL.rootStore.updateVariables({insert variable to modify here})

> Example: ```__SL.rootStore.updateVariables({ username: 'Chris' })```

For the visitor of your Hub, this will replace any occurrences of `{{$$.env.username}}` with the text ”Chris”.

---
**Related Articles**
- [Referencing Other Data Sources](/documentation/referencing-other-data-sources)
- [Publishing](/documentation/publishing)
- [Theming](/documentation/design/theming)
- [Custom CSS](/documentation/design/custom-css)
