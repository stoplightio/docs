# Object Inheritance 

## What 
- A **model** contains common resuable information that can be referenced in your endpoint definitions or other models in your API design. 
- When a model derives its properties from another model, the event is called **inheritance**. 
- The model which contains the common set of properties and fields becomes a parent to other models, and it is called the **base type**.
- The model which inherits the common set of properties and fields is known as the **derived type**.
- If a base type inherits its properties from another model, the derived type automatically inherits the same properties indicating that inheritance is **transitive**. 
- OpenAPI Specification v2 uses the **allOf** syntax to declare inheritance. 
- **allOf** obtains a collection of object definitions validated independently but, collectively make up a single object. 

## Why 
- Inheritance makes your API design more compact. It helps avoid duplication of common properties and fields. 

## Best Practices 

<!-- theme: info --> 
> Avoid using contradictory declarations such as declaring properties with the samer name but dissimilar data type in your base model and derived model. 

### Example 

```
{
  Vehicle: 
    type: object
    properties: 
      brand: 
        type: string 
  Sedan: 
    allOf: # (This keyword combines the Vehicle model and the Sedan model) 
      $ref: '#/definitions/Vehicle'
      type: object
      properties: 
        isNew:
          type: boolean
}
```

