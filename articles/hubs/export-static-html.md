# Download Static HTML & CSS

![Download Static HTML and CSS](https://github.com/stoplightio/docs/blob/develop/assets/gifs/export-static-html.gif?raw=true)

> Requires a Pro Docs plan 

## What?
If you would rather host your documentation outside of Stoplight's hosted servers, you can download a built version of your Hub. Downloading a build will produce a `.zip` containing all of the minified assets necessary to load your Hub. These assets will include HTML, JavaScript, CSS, and JSON files. You will need an HTTP File Server in order to properly view and navigate your downloaded Hub. Any authorizations (Auth0, SAML, etc) you have added will not work, since they require a backend server.

## How to download
1. Click the **Publish** icon on the far left toolbar 
2. Select or create a **domain**
3. Choose a **Hub** or **OAS** file
4. Click the **Build** button to start the build process

> If this is your first build, it will also publish to your selected domain

5. Once your **Hub** has finished building, it will appear in the **Builds** section. Click the download icon to the right of the build
6. Unzip the downloaded `.zip` to view all of the assets. It will most likely be located in your Downloads folder

## How to serve locally on your computer (Mac)
1. Open Terminal and `cd` into the root of your build folder
2. Start your favorite file server (Ex. `python -m SimpleHTTPServer`)
3. Open a web browser and navigate to the file server's local url (Ex `http://localhost:3000`)

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

