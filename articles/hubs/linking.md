# Linking 

## What 
In your Stoplight Hub, linking to different [pages](/documentation/getting-started/pages), [subpages](/documentation/getting-started/subpages), section headers, and external sites allows you to integrate navigation across your docs.  

## How 

We use Markdown style links within Stoplight Hubs. The basic structure of a Markdown link is wrapping the text in `[ ]` and then wrapping the URL in `( )`, like this `[text](URL)`. There are no spaces between the `[ ]` and the `( )`.

> For most links, besides to external sites, you do not need to know the base URL (i.e. https://stoplight.io). Just the path that follows. 

### Pages

If you want to link to a page from another page or subpage, the format will looks like this: 

`[text](/path-to-page)`

For example, if you want to link to the Hello World page. The path is `/hello-world` as set here in the Page Settings: 

![Linking page](https://github.com/stoplightio/docs/blob/develop/assets/images/linking-page.png?raw=true)

The link would look like:

`Check out the [Hello World](/hello-world)`

> Remember: Spaces in the name will be represented by `-`. 

### Subpages 

If you want to link to a subpage from a page or another subpage, you will need to know the path to that subpage starting with the page it is located within. The format will looks like this:

`[text](/path-to-page/path-to-subpage)`

For example, if the Hello World page had a subpage called Getting Started, and then another subpage within that subpage called SDKs that you want to link to: 

![Linking subpage](https://github.com/stoplightio/docs/blob/develop/assets/images/linking-subpage.png?raw=true)

The link would look like:

`Check out our [SDKs](/hello-world/getting-started/sdks)`

### Section Headers

You can link directly to section headers when you are using a `# H1`, `## H2`, or `### H3` heading.

If you are linking to a section header on the page or subpage you are already on, the format will look like this: 

`[text](#header-title)`

If you are linking to a section header on another page or subpage, it will need to include the path followed by `#header-title`. The format will look like this: 

`[text](/path-to-page#header-title)`

> Remember: Similar for paths for pages and subpages, spaces in the name will be represented by `-`. 

### External Sites

If you want to link to an external site, you will use a similar format:

`[text](URL here)`

The only difference is that you will be using the full URL of the site you are linking to. 

For example, a link to the Stoplight homepage would look like: 

`[Stoplight](https://stoplight.io)`

---
**Related Articles**
- [Routing](/documentation/getting-started/routing)
- [Headers](/documentation/getting-started/header-footer)
- [Pages](/documentation/getting-started/pages)
- [Subpages](/documentation/getting-started/subpages)

