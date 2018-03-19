# Preventing Duplications and Simplifying OAS Files 

## What 
- API resources often have or share similar features 
- Duplicating features increase the size and complexity of your API
- Reusable definitions make it easier to read, understand, and update your OAS files
- Similar features can be created as reusable definitions and utilized with references
- These definitions can be hosted on the same server as your OAS file or on a different server 
- You can reference a definition hosted at any location or server 
- Apart from defining reusable definitions, you can also define reusable responses and parameters. You can store your reusable definitions, responses, and parameters in a common library

>Key Terms: A definition is a named schema object. A reference is a path to a declaration within an OAS file

## How to Reference a Definition 
To invoke a reference to a definition, use the **$ref** keyword. For example:
```
#/definitions/Pets ($ref: 'reference to definition')
```

## URL, Remote, and Local References 

### General Syntax for URL Reference
- Reference a complete document or resource located on a different server: 
```
$ref: 'http://url_resource_path'
```
- Reference a particular section of a resource stored on a different server: 
```
$ref: 'http://url_resource_path/document_name.json#section'
```

### General Syntax for Remote Reference
- Reference a complete document or resource located on the same server and location: 
```
$ref:'document_name.json'
```
- Reference a particular section of a resource stored on a different server: 
```
$ref: 'document_name.json#section'
```
### General Syntax for Local Reference
- Reference a resource found in the root of the current document and the definitions:
```
$ref: '#/definitions/section'
```

## Best Practices 
- Only use $ref in locations specifed by the OpenAPI Specification 
- Always enclose the value of your local reference in quotes (when using YAML syntax) to ensure it is not treated as a comment. For example:

Good
```
"#/definitions/todo-partial"
```
Bad 
```
#/definitions/todo-partial
```

## Examples 
- Assuming you have the following schema object named **Todo Partial** and you want to use it inside another definition: 

```
{
  "title": "Todo Partial",
  "type": "object",
  "properties": {
    "name": {
      "type": "string" 
    },
    "completed": {
      "type": [
        "boolean",
        "null"
      ]
    }
  },
  "required": [
    "name",
    "completed"
  ]
}
```
- To refer to that object, you need to add $ref with the corresponding path to your response: 

```
{
  "title": "Todo Full",
  "allOf": [
    {
      "$ref": "#/definitions/todo-partial" (Reference)
    },
    {
      "type": "object",
      "properties": {
        "id": {
          "type": "integer",
          "minimum": 0,
          "maximum": 1000000
        },
        "completed_at": {
          "type": [
            "string",
            "null"
          ],
          "format": "date-time"
        },
        "created_at": {
          "type": "string",
          "format": "date-time"
        },
        "updated_at": {
          "type": "string",
          "format": "date-time"
        },
        "user": {
          "$ref: "https://exporter.stoplight.io/4568/master/common.oas2.yml#/definitions/user" (Reference)
        }
      },
      "required": [
        "id",
        "user"
      ]
    }
  ]
}
    
---
**Related Articles** 
- [Referencing Another API Spec](/modeling/modeling-with-openapi/referencing-another-api-spec)
- [JSON Introduction](/modeling/json-best-practices/introduction)

