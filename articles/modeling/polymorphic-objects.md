# Polymorphic Objects 

## What 

- Resources in your API are polymorphic. They can be returned as XML or JSON and can have a flexible amount of fields. You can also have requests and responses in your API design that can be depicted by a number of alternative schemas. 
- **Polymorphism** is the capacity to present the same interface for differing underlying forms. 
- The **discriminator** keyword is used to designate the name of the property that decides which schema definition validates the structure of the model. 

## Why 
- Polymorphism permits combining and extending model definitions. 

## Best Practices

<!-- theme: warning -->
>The discriminator property **must** be a mandatory or required field. When it is used, the value **must** be the name of the schema or any schema that inherits it. 

### Example 

```
{
  definitions:
  Vehicle:
    type: object, 
    discriminator: brand
    properties:
      model:
        type: string
      color:
        type: string
      required:
    model
    
  Sedan: # Sedan is used as the discriminator value 
  
    allOf:
      $ref: '#/definitions/Vehicle'
      type: object
        properties:
          dateManufactured: 
            type: date
          required: 
            dateManufactured
}
```
