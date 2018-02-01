# API Operations
## Introduction
API operations describe the way you define how an API is exposed to a user. Properly defined operations are fundamental to the API development life cycle and the outcome is a final product that is easy to understand and use. Creating a properly designed RESTful API requires research, analysis, and planning. It is the API developer’s responsibility to ensure that the API design, resources, and connected operations are easy to understand by consumers. The following characteristics are true of well-designed APIs: 

- Comprehensive, yet succinct 
- Understandable and easy to use
- Supports delta (incremental) development
- Expedites and simplifies the API documentation process 

## Key Terms
- A **resource** is an entity or object that has data linked to it, relationships to other objects or entities, and a set of methods that operate on it to access, use, or manipulate the associated data. When resources are grouped together, it is called a collection. 
- A **Uniform Resource Locator (URL)** is used to indicate and identify the location of an API resource and perform some actions to it. Note that the base URL is the constant part of this location. 
- **GET** method requests data from a resource and the body of the response message holds the information requested.  
- **PUT** method requests the server to update the resource or create it (if it does not exist) and the body of the request message indicates the resource to be updated or created.
- **PATCH** method performs a partial update on a resource and the body of the request message indicates the change to be applied.  This can occasionally be more efficient than PUT because the client forwards changes required and not the entire details about the resource. 
- **POST** creates a new resource and the body of the request message indicates the details of the new resource to be created. This method can be used to activate operations that will not create a resource.
- **DELETE** method requests that the specified resource be removed.

## Best Practices

### Resource URL should be based on nouns and not verbs

For example, to retrieve pet details for a pet store which has different kinds of pets:

- /pets (Good) 
- /getAllPets (Bad)

<!-- theme: info -->
> A good resource URL contains resources (nouns) and not actions or verbs. Ensure that the resource is in the plural form at the API endpoint.

### Use HTTP methods to operate on resources

To add, delete, or update information, use the HTTP methods GET, POST, DELETE, PUT, and PATCH (also known as verbs). For example:

- GET /pets (returns the list of all pets)
- GET /pets/5 (returns details of pet 5)

<!-- theme: info -->
> A successful GET method normally returns a HTTP status code of 200 (OK) and 404 (Not found) if the resource cannot be located.

| GET                                   | PUT/PATCH                                     | POST                                | DELETE                                      | Resource               |
|---------------------------------------|-----------------------------------------------|-------------------------------------|---------------------------------------------|------------------------|
| Return list of all pets               | Update all pets                               | Add a new pet                       | Remove all pets                             | path/pets              |
| Return details of treatment for pet 5 | Update all treatment for pet 5                | Add new treatment details for pet 5 | Remove all treatments associated with pet 5 | path/pets/5/treatments |
| Returns details for pet 5             | Updates details for pet 5 assuming it exists  | Error (Not permitted)               | Deletes pet 5 details                       | path/pets/5            |

### Make use of a Query String (?) for complex parameter optional parameters
When you need to add more complexity and dynamics to the request, add parameters to the query string. For example:

- GET /pets?type=feline&age=5 (Good)
- getFelinePets (Bad)

### Utilize HTTP Status Codes 
A user should know the status of request made through an API. This might include failed, passed, or invalid responses. The table below summarizes the codes.

| 2xx Success                                                             | 3xx Redirect          | 4xx Client Error | 5xx Server Error          |
|-------------------------------------------------------------------------|-----------------------|------------------|---------------------------|
| 200 Ok (Success for GET, PUT, or POST)                                  | 301 Moved Permanently | 400 Bad Request  | 550 Internal Server Error |
| 201 Created                                                             | 304 Not Modified      | 401 Unauthorized |                           |
| 204 No Content (Request successfully processed but returns not content) |                       | 403 Forbidden    |                           |
|                                                                         |                       | 404 Not Found    |                           |

- Be wary of using too many status codes and confusing the API user.
- It is good to provide an additional description of the status code in the body of the HTTP Response. For example:
    - Request: method GET /pets?type=feline
    - Response: 
```   
   //This is an invalid request.
    {
    "message": "Invalid Pet Type please enter a valid pet category",
    }
```
### Executing search, sort, filter and pagination operations 
- When you need to perform these actions, you can append the query parameters to the GET method and the API endpoint. For example, to carry out a **search** operation for a particular pet:
    - GET /pets?search=Blaze (This will search for a pet named Blaze)
- **Pagination** helps you to manage the amount of resources you return and it is advisable to use the parameters offset and limit as shown in the example below:
    - GET /pets?offset=10&limit=20 (Return pets between 10 to 20)
- To **sort** the list of resources we can use multiple sort parameters in the query string. For example:
     - GET /pets?sort=age_desc (Would sort the age in descending order.)
- For **filtering** we can use one or more parameters in the query string. For example: 
    - GET /pets?type=canine&age=7 

<!-- theme: info -->
>If too many query parameters are used in GET methods and the URL becomes too long, the server may return a ‘414 URL too long’ HTTP status. Parameters might be passed to the request body of a POST request as a solution to this challenge.

### Versioning 
It is good practice to version an API to describe the available features and resources it exposes. When this is properly done, the application consuming the API can submit explicit requests to a specific version of a feature or resource. For example, you can specify the version of the resource by means of a parameter within the query string affixed to the HTTP request: http://api.yourdomain.com/v2/pets/10/

    

