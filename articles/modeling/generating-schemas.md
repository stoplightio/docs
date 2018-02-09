# Generating Schema 

## What 
- A schema is metadata that defines the structure, properties, and relationships between data. It also defines the rules that must be adhered to and is usually in the form of a document. 
- A structured approach is always recommended for handling and manipulating data. 
- The "$ref" keyword is used to reference a schema. 

## Why 
- A schema definition makes the process of handling data more structured.
- The process of validation and handling user input errors can be imprioved through the use of schemas. 
- Schemas encourage the 'single source of truth' (single place to update a definition) concept which, among other things, makes it easier to create and maintain endpoints. 

## Best Practices 
- It is advisable to always use a schema when you define and implement your API.
- Use schemas to rapidly extract titles, descriptions, and samples for easy API documentation. 

## JSON Schema 
- JSON (Javascript Object Notation) is a popular, human readable data format that is easy to parse at the server or client side. 
- JSON Schema is a standard that contains information about the properties of a JSON object that can be used by an API. It also helps validate the structure of JSON data. 
    -The properties include: name, title, type etc. 
- JSON Schema Specification is divided into three parts: 
  - **JSON Schema Core**: describes the basic foundation of JSON Schema
  - **JSON Schema Validation**: describes methods that define validation constraints. It also describes a set of keywords that can be used to specify validations. 
  - **JSON Hyper-Schema**: an extension of the JSON Schema Specification that defines hyperlink, images, and hypermedia-related keywords. 

## Example 
Assume you have an API that requires data provided in the format below: 

```
{
  pets: [
    {id:1 petName: "Blaze", petType: "Canine", age: 2},
    {id: 2, petName: "Felicia", petType: "Feline", age: 1}
    {id: 2, petName: "Bolt", petType: "Canine", age: 3}
    
  ]
}
```
As seen above, each object in the pets array contains the following properties: id, petName, and petType. You can create a schema definition to validate the data and ensure it is in the expected format. The schema definition is outlined below: 

```
{
  "type":"object",
  "properties": {
    "pets": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {"type": "number"},
          "petName": {"type": "string", "required": true},
          "petType": {"type": "number", "required": true},
          "age": {"type": "number"}
        }
      }
    }
  }
}

### Related Articles 
- [JSON Schema](http://json-schema.org/specification.html) 
