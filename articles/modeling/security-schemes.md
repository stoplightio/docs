# API Security Schemes
API security schemes protect your API resources by authenticating apps or users that consume your API. There are a number of standard authentication protocols you can pick from and each has their own strengths and weaknesses. To help you get started, the section below outlines some common schemes in use.

## Authentication Schemes
### Basic API Authentication
- Easy to implement
- Entails sending encoded username and password details
- Usually bundled with standard framework or language library
- Used with HTTPS, TLS or SSL
- Can be combined with other security methods
- **Note**: this method is susceptible to hijacks and man-in-the-middle attacks

### OAuth1.0 (Digest Scheme)
- Popular, tested, secure, signature driven, protocol
- Uses cryptographic signature, which is a mix of token secret, nonce, and other request based information.
- Can be used with or without SSL

### OAuth2 (Bearer Token Scheme)
- The current OAuth2 specification eliminates need for cryptographic signatures, passwords, and usernames.
- OAuth2 works with authentication scenarios called flows, these flows include:
    - Authorization Code flow
    - Implicit flow
    - Resource Owner Password flow
    - Client Credentials flow
- The OAuth 2.0 server will distribute access tokens that a client application will use to access protected resources.
- [Additional Information on OAuth2.0](https://tools.ietf.org/html/rfc6749)

### OpenID Connect Discovery
- OpenID Connect Discovery (OIDC) is based on the OAuth 2.0 protocol.
- Uses a sign-in flow that permits user authentication and information access by a client app.
- The user information is encoded via a secure JSON Web Token (JWT). 
- [Additional Information on OpenID Connect Discovery](https://openid.net/specs/openid-connect-discovery-1_0.html) 

## Best Practices 
### Implementing IDs
Unique User IDs should be distinctive but not easy to decipher. 
- Example: using ‘a12bc3’ is weak when compared to an ID that reads ‘09dgf659sjf038eyr3367dhrt34j5’. Avoid using auto increment for your Unique User IDs to reduce the likelihood of a security breach. 
### Sensitive Information in HTTP Request 
Ensure that your API will not expose important information such as password, API keys, and security tokens in the URL. For example, this URL is bad because it contains an API key: 
- /baseurl/<uid>q=?apiKey=2123223223 
### API Keys 
Reduce the likelihood of exposing your API keys by keeping them in a file or storage mechanism that is accessible by the owner. 
- **Note**: API Keys can be duplicated or lost so it is important to use other security measures apart from API keys. Consider encryption to make your API keys more secure. 
  
### Validation 
It is beneficial to validate your inputs and access to resources using robust parsers. Parsing requests can help verify the validity of user requests. API designers can perform an implicit input validation to ensure the user inputs data with permitted characters, right syntax and character length. Using regular expressions can also help validate string inputs. If a request exceeds the defined limit, you can return a ‘413 Request Entity Too Large’ response code. 

### Audit log 
Create audit logs before and after security related events. You can also log validation errors to detect patterns or potential attacks.
### HTTP Status Codes 
Use status codes and proper error handling techniques for incoming requests to identify probable security risks.
- [Additional Information on HTTP Status and Error Codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)


