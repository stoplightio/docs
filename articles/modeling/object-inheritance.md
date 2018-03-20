# Object Inheritance

## What

* A **model** contains properties that can be reused and referenced by endpoint
  definitions, shared objects, and other models. For more information on what
  models are and how they can be used, please see the API model overview
  [here](/modeling/modeling-with-openapi/api-models).

* **Inheritance** is when a model derives its properties from another model.

* When a model inherits properties from another model, the model being inherited from is
  known as a **base type** (or parent). A model that is inheriting
  properties from a base type is known as a **derived type** (or child).

* When a base type inherits properties from another model, any derived types
  will also automatically inherit the properties as well. For example, if model
  C is a derived type of model B, and model B is a derived type of model A, then
  model C is also a derived type of model A. In mathematics, this is known as
  the [transitive property](https://en.wikipedia.org/wiki/Transitive_relation).

* To specify that a model should inherit from a base type, use the **allOf**
  option (under "Combination Types") when building the model. By specifying
  allOf and referencing the base type, the model will automatically inherit all
  of the parent model's properties. A model can also inherit from multiple base
  types as needed.

## Why

* Inheritance makes your API design more compact. It helps avoid duplication of
  common properties and fields, reducing the complexity of the specification and the chance of errors.

## Best Practices

> Avoid using contradictory declarations such as declaring properties with the
> same name but dissimilar data type in your base model and derived model.

### Example

As an example, imagine you are creating an API that stores and categorizes
different types of vehicles. To begin working on the API, you will need a base
"car" model with a few attributes that are common across all vehicles. This
might look similar to:

```javascript
// the car base type
{
  "type": "object",
  "properties": {
    // number of wheels
    "wheels": {
      "type": "integer"
    },
    // number of doors
    "doors": {
      "type": "integer"
    },
    // brand of car
    "make": {
      "type": "string"
    },
    // model of car
    "model": {
      "type": "string"
    }
  }
}
```

<!--FIXME Insert image of creating model from UI -->

Now that we have a base type model, we now need a derived type that extends the
base type. Since we're dealing with cars, let's create a model that defines a
SUV type (or a Sport Utility Vehicle):

```javascript
// the SUV model
{
  "allOf": [
    // a reference to the car base type
    {
      "$ref": "#/definitions/car"
    },
    // properties that are only applied to the SUV model
    {
      "type": "object",
      "properties": {
        // whether the vehicle can go "off road"
        "off-road": {
          "type": "boolean"
        },
        // the amount of ground clearance
        "ground-clearance": {
          "type": "integer"
        }
      }
    }
  ]
}
```

<!--FIXME Insert image of creating derived model in UI -->

As shown above, by wrapping our SUV model inside of an `allOf` block, we are
able to include all of the properties that are included in the car base model
above.

When fully de-referenced (the car reference is replaced with the car
properties), the derived SUV model will have the following JSON properties:

```javascript
{
  "type": "object",
  "properties": {
    // number of wheels
    "wheels": {
      "type": "integer"
    },
    // number of doors
    "doors": {
      "type": "integer"
    },
    // brand of car
    "make": {
      "type": "string"
    },
    // model of car
    "model": {
      "type": "string"
    },
    // whether the vehicle can go "off road"
    "off-road": {
      "type": "boolean"
    },
    // the amount of ground clearance
    "ground-clearance": {
      "type": "integer"
    }
  }
}
```
---
**Related Articles** 
- [JSON Introduction](/modeling/json-best-practices/introduction)
- [Adding Validations](/modeling/json-best-practices/adding-validations)
- [Reducing Duplication with $refs](/modeling/json-best-practices/reducing-duplication-with-refs)
- [Generating Schemas](/modeling/json-best-practices/generating-schemas)
