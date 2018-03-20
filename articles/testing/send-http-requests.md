# Overview of Testing with HTTP Requests

## What are HTTP methods?

Hypertext Transfer Protocol (HTTP) is a set of rules that define how information
is requested, transmitted, and formatted between a client and a server. HTTP
methods (verbs) are used to implement create, read, update, and delete
operations on identified resources.

Each HTTP method can be classified as safe, idempotent, or both.

### Safe Methods

Safe methods do not change the state of a resource. Safe methods include:

* **OPTIONS**
* **GET**
* **HEAD**

### Idempotent Methods

Idempotent methods can be called several times and should expect the same
results. Idempotent methods include:

* **OPTIONS**
* **GET**
* **HEAD**
* **PUT**
* **DELETE**

To demonstrate an idempotent HTTP request:

* `GET petAge`, where the returned age is 2. Since the result will always return
  2 when the statement is issued over and over again, this request is
  idempotent
* `POST petAge`, where you are incrementing the age of a pet. Since we are
  actively incrementing the age, each successive execution will give the pet a
  different age each time, making this request non-idempotent

## Methods

* The **GET** method retrieves data and resource representation. It does not
  change the state of a resource and several executions produce the same
  results. Thus, it is a safe and idempotent method. When a GET method is
  successful, it should return a 200 (OK) HTTP status code with the content in
  the response body and a 404 (NOT FOUND) code if the resource is not available

* The **POST** method creates new resources. The POST method is not safe and is
  non-idempotent as the execution of similar POST requests will create two
  different resources with similar details. It is suggested for non-idempotent
  resource requests

* The **PATCH** method makes partial updates to a resource and it is
  non-idempotent

* The **PUT** method updates a resource or creates a new resource if it does not
  exist. It is ideal for the complete update of a resource. The PUT method is
  idempotent but not safe

* The **DELETE** method deletes a resource. It is idempotent, but not safe

## Testing with HTTP Requests

Testing using HTTP Requests demonstrates whether or not an API will perform as
expected when it is deployed to a production server and integrated with existing
platforms.

> HTTP Request Tests should include checks to the response code, message, and body.

Apart from verifying the functionality of essential features, HTTP Request Tests
**save time and cost**.

## Testing with HTTP Requests: Best Practices

Testing is a critical stage of the API development life cycle and the type of
tests executed will depend on the complexity of the API, time, budget, etc. It
is vital to conduct robust tests to reveal any inconsistencies or defects in
the API before it is shipped to a production server or interfaced with other
platforms.

### GET

* Test the GET method to confirm it returns the correct data
* Test a valid GET request to ensure it returns a 200 (OK) status code or 404 (NOT FOUND) if invalid
* Ensure you test every endpoint fetching data within your API before deployment to a production server

### POST

* Test the POST method to confirm it creates a resource and returns a 200(OK)
  code and/or 201(CREATED) code if valid. If invalid, look for a 4xx error
  status code
* You can use the GET method to see the outcome of the POST operation

### PUT & PATCH

* The PUT and PATCH update methods should be tested to ensure that a 200(OK)
  status code or 204(NO CONTENT) is returned for a successful transaction. If
  unsuccessful, look for a 4xx error status code

### DELETE

* Test the DELETE request to certify it returns a 4xx error code if a DELETE
  operation is executed against an invalid or non-existent resource
* Test the DELETE request to confirm it returns a 200(OK) for a successful
  operation
* Tests for the DELETE method **must not** be done with data residing on a
  production or live data store
  
  ---
  **Related Articles**
- [Testing Introduction](/testing/introduction)
- [Passing Data Between Steps](/testing/getting-started/passing-data-between-steps)
- [Running Tests In Stoplight](/testing/running-tests/in-stoplight)
- [Running Tests in the Terminal](/testing/running-tests/in-the-terminal)
- [Running Tests Triggered by URL](/testing/running-tests/triggering-by-url)

