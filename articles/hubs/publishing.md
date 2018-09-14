# Publishing

![Publishing](https://github.com/stoplightio/docs/blob/develop/assets/gifs/documentation-publishing.gif?raw=true)

## What

Publishing your documentation has never been easier. Stoplight has added:

- New **Integrations** for Segment, Intercom, and Google Analytics to allow for traffic monitoring and additional analytics
- New **Authorizations** to make sure your documentation is secure at all times. This includes basic user/password authentication and SSO provider integration, powered by Auth0, SAML, and more.
- New **Builds** section for tracking published Hubs, including when a Hub was published, who published it, and under what domain.

> Take that Gutenberg!

## Who

- **Organization Owners**, **Account Owners**, and **Administrators** can publish Hubs

## How

1.  From the Stoplight editor, click on the **Publish** icon in the far left-hand toolbar
2.  Input a **subdomain** under Stoplight's ```.docs.stoplight.io``` domain
    - Or input a **custom domain** as shown below (optional)
3.  Once completed, click **Next ->**
4.  Select the Hub you wish to publish under **Hub File**
    > Publishing will use the latest version of the selected file (denoted by a star in the versions list) 
5.  Add Integrations to **Segment**, **Intercom**, and **Google Analytics** under Integrations (optional)
6.  Add security via **Username/Passwords Login**, **Auth0**, or **SAML** (optional)
7.  Once completed, click **Publish** in the top left
8.  A confirmation window will ask you to confirm your selection, click **Okay**
9.  Once confirmed, **Build Logs** will display your current progress
    - The process usually takes 2-5 minutes
10. Once the process has completed, a **green success message** will display at the bottom of the screen, letting you know that the Hub was published succesfully
11. Once a Hub is published, it will appear under **Builds**
12. To unpublish a Hub, select **Unpublish** in the **Danger Zone** underneath **Builds**
    - If you wish to delete all builds and release the domain you are currently using, select **Remove Domain**
    
### Custom Domains 
1. Click on the **Publish** icon in the far left-hand toolbar 
2. Select the **Custom?** checkbox 
3. Input your **custom domain** in the text field and click **Next**
4. Create a **DNS CNAME** Record 
3. Point your custom domain to ```ingress.docs.stoplight.io``` before you publish 

---

**Related Articles**

- [Documentation with Hubs](/documentation/introduction)
- [Routing](/documentation/getting-started/routing)
- [Headers](/documentation/getting-started/header-footer)
- [Pages](/documentation/getting-started/pages)
- [Subpages](/documentation/getting-started/subpages)
- [Blocks](/documentation/blocks)
