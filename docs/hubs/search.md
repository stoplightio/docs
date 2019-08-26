# Hub Search 

![Hub Search](https://github.com/stoplightio/docs/blob/develop/assets/imagesv2/Hub%20Search.png?raw=true)

Stoplight provides a search engine for documentation published with Stoplight. Hub search enables easy access to specific content using keywords and tags. 

## How it Works 
When you publish your documentation, every page in your Hub is indexed. The index file that is created sorts content by keywords, avoiding prepositions and other non-specific language. The search will display the first 150-200 words of each page with matching content. Search results are ranked by how often the term appears on a page.

### Features 
- Instant Search Results 
- Generated Index file is included with your built Hub 
- Search is served up on each page 
- Search enabled offline 
- Full context search 
- Tags will appear in search results 
- Indexes alt-text for images

### Custom CSS 

#### Hide Hub Search 
```.HubHeader-search {display: none;}```

#### Change Search Highlight Color 
```.HubSearch-match {Background-color: rgba(255,255,0,.75);}```

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
