# Authorization 

## What is Authorization? 
 
- **Authentication** is the process of verifying if a user or API consumer can have access to an API. 
- **Authorization** defines the resources an authenticated (properly identified) user can access. For example, a user might be authorized to use an endpoint for retrieving results but denied access to the endpoint for updating a data store. 
- Authentication strategies can be implemented using basic HTTP authentication or OAuth methods. Authorization can be implemented using roles and claims. 

## Authentication Schemes 
- **Basic Authentication** is easy to implement and utilizes HTTP headers to validate API consumers. While the credentials might be encoded, they are not encrypted. It is advisable to use this method over HTTPS/SSL. 
- **OAuth 1.0** has its foundation in cryptography. Digital signatures are used to authenticate and ensure the data originates from an expected source. It can be used with or without SSL. 
- While OAuth 1.0 works primarily with web clients, **OAuth 2.0** works with web and non-web clients. OAuth 2.0 is easy to implement and focuses on bearer tokens. It wokrs with HTTPS/SSL for its security requirement. 
- **AWS Signature** is a secutiry protocol that defines authentication information added to AWS requests. It consists of an access key ID and a security access key. Users who generate manual HTTP requests to AWS are required to sign the requests using AWS Signature. [Click here to learn more about AWS Signature](https://docs.aws.amazon.com/AmazonS3/latest/API/sig-v4-authenticating-requests.html)

## Best Practices for Authentication and Authorization when Testing APIs

- Use the same authentication and authorization your users would use during testing. Doing so will help you effectively identify and resolve issues users might face in a live scenario. 
- Avoid creating too many test accounts with administrative access to all endpoints and resources during your test phase. It can be exploited, putting your resources and data at risk when the API is avaialble to consumers. 
- Use ecryption to store valid IDs and credentials. Ensure test procedures containing valid user IDs or tokens are not displayed as unmasked text in test results or test logs. 
- Test your authentication and authorization procedures rigorously by attempting to access secured resources with invalid credentials or session tokens or by atttempting to access a resource denied to an authenticated user. 
