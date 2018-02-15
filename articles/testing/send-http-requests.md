# Overview of Testing with HTTP Requests 

## What are HTTP methods? 

- Hypertext Transfer Protocol (HTTP) is a set of rules that define how information is requested, transmitted, and formatted between a client and a server. HTTP methods (verbs) are used to implement create, read, update, and delete operations on identified resources. 
- HTTP methods are classified as safe, non-safe methods, idempotent or non-idempotent methods. Safe methods do not change the state of a resource. Idempotent methods, if executed severally, deliver consistent outcomes. An example of idempotency is outlined below:

### Example 
- petAge = 2 # will always return 2 even when the statement is executed over and over again. This statement is idempotent. 
- petAge++ # will return different results based on the number of executions. This statement is non-idempotent. 

## Methods
- The **GET** method retrieves data and resource representation. It does not change the state of a resource and several executions produce the same results. Thus, it is a safe and idempotent method. When a GET method is successful, it should return a 200 (OK) HTTP status code with the content in the response body and a 404 (NOT FOUND) code if the resource is not available. 
- The **POST** method creates new resources. The POST method is not safe and is non-idempotent as the execution of similar POST requests will create two different resources with similar details. It is suggested for non-idempotent resource requests. 
- The **PATCH** method makes partial updates to a resource and it is non-idempotent. 
- The **PUT** method updates a resource or creates a new resource if it does not exist. It is ideal for the complete update of a resource. The PUT method is idempotent but not safe. 
- The **DELETE** method deletes a resource. It is idempotent but not safe. 

### Summary 
The GET method is the only safe method, as it does not change the state of a resource. GET, PUT, and DELETE methods are idempotent while the POST and PATCH methods are non-idempotent. 

## Testing with HTTP Requests 
- Testing using HTTP Requests demonstrates whether or not an API will perform as expected when it is deployed to a production server and integrated with existing platforms. 

<!-- theme: info -->
> HTTP Request Tests should include checks to the response code, message, and body.

- Apart from verifying the functionality of essential features, HTTP Request Tests **save time and cost**.

## Testing with HTTP Requests: Best Practices 

### GET
- Test the GET method to confirm it returns the correct data.
- Test a valid GET request to ensure it returns a 200 (OK) status code or 404 (NOT FOUND) if invalid 
- Ensure you test every endpoint fetching data within your API before deployment to a production server. 

### POST
- Test the POST method to confirm it creates a resource and returns a 200(OK) code and/or 201(CREATED) code if valid. If invalid, look for a 4xx error status code. 
- You can use the GET method to see the outcome of the POST operation. 

### PUT & PATCH
- The PUT and PATCH update methods should be tested to ensure that a 200(OK) status code or 204(NO CONTENT) is returned for a successful transaction. If unsuccessful, look for a 4xx error status code. 

### DELETE
- Test the DELETE request to certify it returns a 4xx error code if a DELETE operation is executed against an invalid or non-existent resource. 
- Test the DELETE request to confirm it returns a 200(OK) for a successful operation. 
- Tests for the DELETE method **must not** be done with data residing on a production or live data store. 

<!-- theme: info -->
> Testing is a critical stage of the API development life cycle and the type of tests executed will depend on the complexity of the API, time, budget, etc. It is vital to conduct robust tests to reveal any inconsistencies or defects in the API before it is shipped to a production server or interfaced with other platforms.  
