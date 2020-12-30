# Custom Javascript 

Adding custom Javascript to your documentation allows you to further customize the functionality and aesthetic. Utilize Javascript elements like components, animations, and visual effects to make unique, in-depth documentation. 

![Custom Javascript Publish Panel](https://github.com/stoplightio/docs/blob/develop/assets/imagesv2/custom-js.png?raw=true) 

There are two ways to add custom JS to your documentation: through the Publish panel or directly to HTML components of your Hub. Both are discussed below.

## Publish Panel

1. Open the **publish panel** on the left-hand sidebar of your project screen
2. Select **Custom Javascript** from the **Advanced** section
3. Input Javascript within the panel, which will be added to the ```<head>``` tag of every page

### Importing External Libraries

To import an external or third-party Javascript library, use the custom Javascript below in the **Custom Javascript** input from the publish settings:

```js
function addCustomScriptToBody() {
  var script = document.createElement("script");
  script.src = "https://cdn.example.com/my-custom-code.js"; // FIXME update this to the URL of your javascript
  document.body.appendChild(script);
}

window.addEventListener("DOMContentLoaded", addCustomScriptToBody, false);
```

Be sure to update the `src` URL above to point to the target Javascript library.

## Custom HTML Pages and inline HTML Blocks 

1. Create an **HTML page** or **inline HTML block** for your Hub
2. Add ```<script>``` tags directly to the page with the desired Javascript

---
**Related Articles**
- [Documentation with Hubs](/documentation/introduction)
- [Routing](/documentation/getting-started/routing)
- [Pages](/documentation/getting-started/pages)
- [Subpages](/documentation/getting-started/subpages)
- [Blocks](/documentation/blocks)
- [Referencing Other Data Sources](/documentation/referencing-other-data-sources)
- [Publishing](/documentation/publishing)
- [Theming](/documentation/design/theming)
- [Custom CSS](/documentation/design/custom-css)
- [OAuth 2.0 for Hubs](/documentation/authorizations/oauth-hubs)
