# Introduction to JSON

## What is JSON?

JSON (short for JavaScript Object Notation) is a syntax used to represent data
structures in a simple, easy-to-read textual format. JSON is ubiquitous
throughout the computing industry, and has become the de-facto data format of
the Web.

If you have never seen JSON before, here is a small demonstration using JSON to
describe a (fictional) person:

```json
{
  "firstName": "Lando",
  "lastName": "Calrissian",
  "title": "Baron Administrator",
  "address": {
    "streetAddress": "123 Betrayal Dr",
    "city": "Cloud City",
    "planet": "Bespin"
  },
  "homeworld": "Socorro",
  "currentLocation": null
}
```

## Why JSON?

There are many benefits to using JSON, some of which include:

* It can be used to represent a wide array of objects in a simple and
  easy-to-read format, making it useful for just about anything.

* It is widely used and supported across web browsers and programming languages,
  making it very easy to develop for.

* It is easy to read and write by humans (as well as computers), making it a
  great choice for specifications like [OpenAPI](https://github.com/OAI/OpenAPI-Specification#the-openapi-specification).

* It is a subset of another syntax called
  [YAML](https://en.wikipedia.org/wiki/YAML). Documents written in JSON can also
  be written in YAML, so either format can be used to write OpenAPI documents.

* It can be used to link files together through [JSON
  references](./reference-spec.md), making it easy to break up large documents
  into smaller, more focused documents.

Whether you are modeling an API, creating a Prism Collection, or writing
documentation in Stoplight, behind the scenes you are actually updating a JSON
document.

<!-- theme: info -->

> You can see the underlying JSON document of any object being updated in
> Stoplight using the editor's **Code** button at the top of the screen.

---

**Related**

* [JSON Overview - Wikipedia](https://en.wikipedia.org/wiki/JSON)
* [YAML Overview - Wikipedia](https://en.wikipedia.org/wiki/YAML)
* [OpenAPI Specification Format Reference](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md#format)
* [Referencing Another API Specification](./reference-spec.md)
