# Introduction to Objects in API Document Structure 

- An OpenAPI document is a document that describes an API and conforms to the OpenAPI Specification. These documents can be in YAML or JSON format. 
- Your OpenAPI document can be a single document or a combination of several associated resources which use the $ref syntax to reference the interrelated resources. 

## Primitive Data Objects Supported in an OpenAPI Document

- integer (int32 and int64)
- number (float and double) 
- string 
- byte
- binary 
- boolean 
- date
- dateTime
- password 

## Additional OpenAPI Objects 

- **Info Object**: describes the API's title, description (optional), and version metadata. It also supports other details such as contact information, license, and terms of service. 
- **Server Object**: identifies the API server and base URL. You can identify a single server or multiple servers and describe them using a description field. All API paths are relative to the URL of the server, for example, "/pets" when fully dilineated, may describe "http://api.hostname.com/pets." 
- **Paths Object**: outlines relative paths to individual endpoints within your API and the operations or HTTP methods supported by the endpoints. For example, "GET/pets" can be used to return a list of pets. 
- **Parameter Object**: describes a single operation parameter. Operations can have parameters passed through by several means such as: URL path, query string, cookies, and headers. Parameters can be marked as mandatory or optional, you can also describe the format, data type, and indicate its depreciation status. 
- **Request body object**: describes body content and media type. It is often used with insert and update operations (POST, PUT, PATCH).
- **Response object**: describes the expected response which can be referenced using the $ref syntax or described within the document. It associates an HTTP response code to the expected response. Examples of HTTP status codes incldue the 200-OK or 404-Not Found codes. [Click here for more information on HTTP Response codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).
