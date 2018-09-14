# Custom CSS

![Applying Custom CSS](https://github.com/stoplightio/docs/blob/develop/assets/gifs/hubs-custom-css.gif?raw=true)

## What 

Want to add some style and flair to your documentation? Add your own custom CSS to enhance your Hub’s look and feel. Below are some of the classes you can modify: 

```
.Hub
  .HubHeader
    .HubHeader-section
      .HubHeaderItem.is-active
        .HubHeaderItem-name
  .HubMain
    .HubSidebar-overlay
    .HubSidebar-wrapper
      .HubSidebar
        .HubSidebar-inner
      .HubBranding
    .HubPage-wrapper
      .HubPage
        .HubPage-inner
          .HubPage-content
            .HubPageCrumbs
              .HubPageCrumb 
            .HubPageBody 
              .HubBlock
            .HubPageFooter
```

## How

1. Select the Hub you wish to modify 
2. Select the **Design View**
3. Click on **Theme** in the top toolbar 
4. Select **Custom CSS** in the bottom left 
5. Input CSS in the text area at the bottom of the page 
6. Input CSS in the generated **theme** file (optional)
7. In publishing, check the **Custom CSS** box under **Advanced** to apply the Custom CSS to that Hub when published

>After accessing Custom CSS, a **theme** file will be generated under Documentation in the file explorer. After making changes to your CSS, make sure to save the **theme** file. 

---
**Related Articles**
- [Theming](/documentation/design/theming)
