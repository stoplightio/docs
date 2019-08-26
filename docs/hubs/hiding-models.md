# Hiding OAS Models 

![Hiding Models](https://github.com/stoplightio/docs/blob/develop/assets/imagesv2/hiding-models.png?raw=true)

## What
Remove OAS models from your documentation and Read View. 

## How 
1. Select the modeling file you want to modify 
2. Switch to **Code View**
3. Add the following code to the root of your OAS spec 

```
"x-stoplight": {
    "docs": {
      "showModels": false
    }
  },
```
4. Refresh the web app to see the changes take effect 
---
**Related Articles**
- [Documentation with Hubs](/documentation/introduction)
- [Routing](/documentation/getting-started/routing)
- [Headers](/documentation/getting-started/header-footer)
- [Pages](/documentation/getting-started/pages)
- [Subpages](/documentation/getting-started/subpages)
- [Blocks](/documentation/blocks)
- [Referencing Other Data Sources](/documentation/referencing-other-data-sources)
- [Publishing](/documentation/publishing)
- [Theming](/documentation/design/theming)
- [Custom CSS](/documentation/design/custom-css)
- [OAuth 2.0 for Hubs](/documentation/authorizations/oauth-hubs)
	
