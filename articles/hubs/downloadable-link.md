# Expose a Downloadable Version of your API Specification 

![Download Link](https://github.com/stoplightio/docs/blob/develop/assets/imagesv2/download-spec-link.png?raw=true)

## What 
Expose an easily accessible downloadable version of your API Specification in published documentation via a link. 

## How 
There are two methods for adding a downloadable version 

![Include link in documentation](https://github.com/stoplightio/docs/blob/develop/assets/imagesv2/download-link.png?raw=true)

### Within a Documentation File 
1. Select the **documentation file** you want to modify 
2. Reference an **OpenAPI File** in your documentation file 
3. Check **Include Download Link?** 

### Via Specification Extension 
1.  Select the **modeling file** you want to modify 
2. Select **code view**
3. Add the extension ```x-stoplight: { docs: { includeDownloadLink: true } }``` to your API Specification 

---
**Related Articles**
- [Documentation with Hubs](/documentation/introduction)
- [Routing](/documentation/getting-started/routing)
- [Referencing Other Data Sources](/documentation/referencing-other-data-sources)
- [Publishing](/documentation/publishing)
- [Theming](/documentation/design/theming)
- [Custom CSS](/documentation/design/custom-css)
- [OAuth 2.0 for Hubs](/documentation/authorizations/oauth-hubs)


