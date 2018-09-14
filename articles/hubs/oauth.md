# OAuth 2.0

## What

If your API is protected by OAuth, you will need to enable it for Try It Out. Enabling OAuth for Try It Out can be accomplished through two different methods: via Modeling or directly into the Hubs code.

## How

### Hubs

![OAuth in Hubs](https://github.com/stoplightio/docs/blob/develop/assets/images/hubs-oauth-code.png?raw=true)

1.  Select the Hub you wish to modify
2.  Select **Code View**
3.  Add the following lines of code to your Hub:

```
"config": {
  "http": {
    "oauth2": {
      "credentials": {
        "flow": "insert grant_type flow here"
        "authorize_url": "insert authorize url here",
        "access_token_url": "insert access token url here",
      }
    }
  }
}
```

> If no flow is stated, defaults to access code

---

**Related Articles**

- [OAuth](/modeling/modeling-with-openapi/oauth)
- [Digital Oceans: Introduction to OAuth2](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2)
- [Security Schemes](/modeling/modeling-with-openapi/security-schemes)
