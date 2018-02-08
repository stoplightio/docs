# OpenAPI Validation

![](../../assets/gifs/file-validation-oas-spec.gif)

## What
OpenAPI validation is the process of verifying the underlying OpenAPI file syntax by making sure it conforms to the [OpenAPI Specification requirements](https://github.com/OAI/OpenAPI-Specification#the-openapi-specification) provided by the [OpenAPI Initiative](https://www.openapis.org/). Stoplight immediately validates any changes done to a spec to ensure they are in the correct format prior to being saved.

<!-- theme: info -->
> Stoplight currently supports the OpenAPI v2 specification. We are working on support for OpenAPI v3, and should have more information in the coming months.

## Why 
- Validation promotes data integrity in your data store. For example, a user making updates during a PUT operation might omit data for an important property and overwrite valid data, compromising data integrity. 
- Validations indicates that you are engaging in good design practice and your API design is consistent. 

## Best Practices 
- All requests made to an API should be validated before processing
- Mark all mandatory properties as **Required** to ensure that the value of the property is provided 
- Assign a default value to optional properties or parameters with missing values. The server will use the default value when a value is missing or not provided 
- You can use the keyword **ReadOnly** to designate a property that can be sent in a response and should not be sent in a request

<!-- theme: info -->
> Using a default value is not recommended when a property or parameter is mandatory

- An API can comsume different media types, the accepted media type can be specified using the **consume** keyword at the operational level or root level to define acceptable media types. For example: 

```
consumes: 
multipart/form-data
or
consumes:
application/json
```
- An HTTP response containing a user friendly error description is useful when validation fails
***

**Related**

* [File Validation](../editor/file-validation.md)
