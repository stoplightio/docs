# OAuth for Hubs 

## What 

OAuth provides a level of security to your documentation to restrict access to it. If your API is protected by OAuth, you will need to enable it for Try It Out. Enabling OAuth for Try It Out in Hubs can be accomplished through two different methods: via Modeling or directly into the Hubs code.

> Stoplight supports OAuth 1.0 and 2.0 

## How 

### Modeling 

![OAuth in Modeling](https://github.com/stoplightio/docs/blob/develop/assets/images/hubs-oauth-modeling.png?raw=true)

1. Create a new Modeling file or select an existing one referenced by the Hub you wish to modify 

> If you are creating a new Modeling file, make sure to reference it in your Hub 

2. Next to **Security** in the left-middle toolbar, Add a Security Scheme by clicking the **+**
3. Input a **key**
4. Select oauth2 under **type** 
5. Select **accessCode** under OAuth **flow** 
6. Select an **authorization url**
7. Select a **token url** 
8. **Add Scope** (optional) 
9. Add a **Security scheme description** (optional)

### Hubs 

![OAuth in Hubs](https://github.com/stoplightio/docs/blob/develop/assets/images/hubs-oauth-code.png?raw=true)

1. Select the Hub you wish to modify 
2. Select **Code View**
3. Add the following lines of code to your Hub:

```

"config": {
  "http": {
    "oauth2": {
      "credentials": {
        "authorize_url": "insert authorize url here",
        "access_token_url": "insert access token url here",
      }
    }
  }
}

```

---
**Related Articles**

- [Digital Oceans: Introduction to OAuth2](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2)
- [Security Schemes](/modeling/modeling-with-openapi/security-schemes)

