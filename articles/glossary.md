# Glossary 

## General Terms 

**Reference**: A JSON Reference allows a JSON value to reference another value in another JSON document. 

**Headers**: Carries information between a client and a server during a Request or a Response.

**minLength**: An attribute used to constrain the length of a string. The length of a string instance must not be less that the minLength when used. 

**maxLength**: The length of a string instance must not exceed maxLength when used. 

**Pattern**: indicates that a string should be a valid regular expression. 

**Allow empty value**: Indicates if an empty value is acceptable. 

**Enum**: List of allowed values. 

**Body**: Data transferred in HTTP message following the Header.

**Validation**: A linter that checks the accuracy of JSON files and/or data. 

**API key**: A special token used to indicate the origin of a request. 

**Metadata**: Data that describes and gives information about data. 

**String**: Double-quoted Unicode characters. 

**Array**: An ordered sequence of values. 

**Object**: An unordered collection of key:value pairs. Objects in JSON are surrounded by curly braces {}. 

**Integer**: Digits from 0-9. Can be negative or positive. 

**Boolean**: True or False 

**Null**: A data type that indicates an empty value. Supported by JSON. 

**Response Codes**: These are HTTP status codes made a server as a response to a client's request. 

### Authorization 

**Basic Auth**: An authentication scheme that utilizes HTTP headers to validate API consumers. Utilizes Base64 encoding. 

**Digest Auth**: Similar to Basic Authentication, but applies a hash function to encrypt the username and password before sending them over the network. 

**OAuth 1.0**: OAuth 1.0 makes use of digital signatures to authenticate and ensure the data originates from an expected source. It can be used with or without SSL. 

**OAuth 2.0**: OAuth 2.0 authentication scheme expands upon 1.0 with a concentration on bearer tokens. It works with HTTPS/SSL for its security requirements. 

**AWS Signature**: A digital security signature included in the authentication information send in a request. It is used by AWS to verify the identity of the requestor. 

## General Platform 

**Organizations**: Organizations function as a shared space for you and your co-workers. Organizations are ideal for grouping people, data, and billing together in one convenient location.

**Teams**: A Team is a collection of people with common interests. Teams make it easier for Organization Members to collaborate and allow you to have additional control over permissions. 

**Project**: A Project is the workspace of the Stoplight Platform. 

**Lifecycle Tags**: These tags help you effectively organize the various stages of your API development process. 

**Change Log**: Record of all significant changes made to a Project. 

**Project Private/Public**: Describes the visibility status of a Project. A Public Project can be viewed by anyone, when a Project is Private, the Project Owner determines who can view the Project. 

## Editors 

**Tokens**: Unique identiier used to authenticate a consumer or application requesting access to an API. 

**API Reference**: Documentation containing what you need to know to use or work with an API.

**HTTP Request Maker**: Used to create a request to operations defined in an API. Also returns the response from requests. 

**Powering a Page**: This feature allows you to integrate a specification into a Hub's Page or Subpage. Ideal for integrating information from an external data source to drive the content shown on a Hub page. 

**Path Parameter**: A path parameter is the variable part of a URL path and it is often used to point to a specific resource within a collection. A URL can have one or more path parameters with each parameter represented by a pair of curly braces {}.

**Query Parameter**: These are parameters in the query string that appear at the end of the request URL after a question mark (?, with different name=value pairs separated by an ampersand (&).

**Models**: Models describe common structures in your API design. Models help reduce duplication in your API definitions and increases future maintainability. 

**Shared Models**: Models that can be used in several APIs across your projects. 

**Config**: Contains configuration details about the API and lists the version number. 

### File Types 

**YAML**: YAML is a human friendly, unicode based, data serialization standard for all programming languages. Also referred to as 'YAML Ain't Markup Language' or 'Yet Another Markup Language.' 

**.oas2**: File extension indicating the file is an OAS2 (Swagger 2) file. You can create an OAS2 file with the Design Editor in Stoplight NEXT. 

**.hub**: File extension indicating file is a technical documentation file. Stoplight's Hubs creates .hub files. 

**.prism**: File extension indicating file is a Prism file. 

**.md**: File extension indicating file is a markdown file. 

## Hubs 

**Sidebar Token**: This is an extra, compact CSS customization for Hubs. Ideal for adding a short token for use in the sidebar of a Hub.

**Page**: Basic elements of a Hub. They function as the starting point for any Hub and each page is automatically added as a link in the Hub's header. 

**Subpage**: Nested pages within a page. You can have subpages nested within a subpage. 

**Blocks**: Editors for creating elements that make up your Hub. 

**Markdown**: Markdown is a text-to-HTML conversion tool for web writers. Markdown allows you to write using an easy to read/write text format, then convert it to structurally valid XHTML (or HTML).

## Designing 

**CRUD builder**: Used to create all relevant CRUD operations for a defined model. 

**API base path**: The base path on which an API is served relative to the host. 

**Version**: Indicated the version of the API (should not be confused with specification).

**Terms of Service URL**: URL to the Terms of Service for an API. 

### Global Settings 

**Supported Schemes**: This is the transfer protocol for the API. Supported protocols include HTTP, HTTPS, WS, and WSS. 

**Request MIME Types**: A list of MIME types the API can consume. This is global to all APIs but can be overridden on specific API calls. 

**Response MIME Types**: A list of MIME types that API can produce. This is global to all APIs but can be overriden on specific API calls. 

**Global Security**: Security schemes that you can use globally and in operations. 

**Contact**: Contact name, email, and URL for contact person or organization. 

**License**: Includes deatils for license name and URL for the license used by the API. 

### Security 

**Key**: This is a special key property for the secutiry definition. It must be unique to the specification. 

**Type**: Describes the type of security scheme used in the API. Includes: Basic, APIKey, and OAuth2 security schemes. 

**In**: Indicates the location of the API key. This could be in the query or header. 

**Name**: The name of the header or query parameter to be utilized. 

### Paths 

**operationID**: Unique string that identifies an operation. The value of the operationID must be unique among all operations described in the API. 

**Deprecated**: This property indicates an operation is deprecated. 

**Consumes**: Describes the MIME types an operation can consume.

**Produces**: Describes the MIME types an operation can produce. 

## Scenarios 

**Before Scenario**: Lists the scenarios that are run before the main collection scenarios. 

**After Scenario**: Lists the scenarios that are run after the main collection scenarios. 

**Utility Scenario**: Used to de-duplicate common tasks. They are not run with the scenarios in your collection and can be referenced from other scenarios. 

**Collection**: This is a top level object that holds many scenarios. 

**Trigger This Collection**: This section gives you options for running your collection. You can choose to trigger your collection through Prism or, a specific URL within Stoplight Scenarios. 

### Swagger/OAS Coverage 

**Coverage**: The Coverage Report gives you a quick overview of the parts in the connected specs covered by test assertions in the current Scenarios Collection. 

**Contract Test Settings**: Indicates the API involved in the contract testing process.

**2xx Code Asserted**: Defines the list of expected 2xx status codes. 

**All Codes**: Defines the list of expected status codes. 

### Run Result 

**Assertions**: This property indicates the number of assertions within a Collection. 

**Passed**: This property indicates the number of succesful assertions within an executed Collection. 

**Failed**: This property indicates the number of failed assertions within an exectued Collection.

**Time Taken**: This property indicates the amount of time taken to execute a Collection. 

**Slowest Scenario**: A scenario with the lowest execution time. 

**Output**: Full object that is returned after running a Scenario. 

### Scenario Config 

**ID**: Unique ID for identifying a scenario 

**Stage**: Describes the level the scenario resides in. It includes Before, Scenarios, After, and Utilites. 

**$$.env**: This object gives you access to environment variables. 

### Steps 

**HTTP/Script/Reference**: Outlines different step types available in a Scenario. A step can be one of three types: HTTP, Script, or Reference. 

**$.ctx**: This variable is used for passing data in between steps. 

**Scripts**: Scripts are used to enhance your conditional logic or processing and gives you access to the $.ctx variable. 

**Original Request**: Shows the HTTP Request as it was sent, after all transformations, scripts, and variable replacements were run. 

**Utilites**: Utility scenarios are used to de-duplicate common tasks and you can reference them from other scenarios. 

## Prism 

**Prism**: Prism is a performant, dependecy free server, designed specifically to work with web APIs. 

**Mock Server**: Prism understands OpenAPI and can act as a mock server, routing incoming requests to example responses, or dynamically generating examples on the fly. 

**Prism Instance**: A Prism Instance is a specific implementation of the Prism server. It can be executed locally or from a hosted location. 

**APIS**: List of APIs used to match incoming requests, which can then be forwarded to upstream servers. 

**Upstream URL**: Indicates the URL that will receive forwarded requests. 

**Methods**: Used to indicate the methods that will be matched in forwarded requests. 

**Hosts**: IP address (IPv4) or domain name that serves the API. 

**Paths**: Includes related endpoints exposed by an API. 

**Connected Specs**: This feature is used for linking related specification files. You can connect to specification files internally or externally. 

### Matched Rules 

**Before**: Before Rules are executed on incoming traffic before it gets to the end API server. 

**After**: After Rules are executed on traffic coming back from the end API. 

**Done**: Rules in the phase are executed after the rules for the incoming and outgoing traffic. 

## JSON/OpenAPI Terms 

**Swagger**: A specification for documenting and defining REST APIs (See OAS Specification) 

**OAS**: Acronym for Open API Specification, previously known as Swagger, a psecification for documenting and defining REST APIs

**OpenAPI**: Synonymous with OAS. Differences between v2 and v3 include: changes to the URL structure and extended JSON Schema support. v3 includes: "oneOf", "anyOf', "not", "nullable", "deprecated", and "writeOnly" properties. 

**OAS Specification**: machine-readable interface files for descriging, designing, consuming, and visualizing RESTful APIs. 

**REST**: Acronym for Representational State Transfer, an architectural style for developing web services. 

**SOAP**: Acronym for Simple Object Access Protocol, a lightweight protocol for exchanging information in a decentralized, distributed environment. 

**GraphQL**: A data query language for APIs 

**JSON**: Acronym for JavaScript Object Notation, a simple data interchange format. 

**Responses**: A server's reply to a request. Usually conists of a status code, reason phrase, and other elements. 

**Schema**: A declarative format that describes the structure of other data. 

**Required**: A value or a definition that is an absolute requirement and must be provided.

**Endpoints**: An endpoint is an entity or resource that can be referenced and is usually represented as the URL of a server or service. 

### Requests 

**GET**: HTTP method used for requesting or retrieving data from a specific resource. 

**PUT**: HTTP method for overwriting a representation of a specific resource or creating a new resource if it does not exist. 

**POST**: HTTP method used to create a new resource. 

**PATCH**: HTTP method for making partial updates to a resource. 

**DELETE**: HTTP method for deleting a specific resource. 

## Formats 

**Int32**: A 32-bit signed integer 

**Int64**: A 64-bit signed integer 

**Float**: Single-precision 32-bit floating point number 

**Double**: Double-precision 64-bit floating point number 

**Byte**: Base64-encoded string of bytes 

**Binary**: Sequence of octets or bytes storing raw-byte data 

**Date**: RFC3339 date format given as YYYY-MM-DD 

**Date-time**: RFC3339 timestamp in UTC time gives as YYYY-MM-DDThh:mm:ss.fffZ. The milliseconds segment (.fff) is optional 

**Password**: String data type with masked format for UI to hide an input

**Email**: String data type with email format



