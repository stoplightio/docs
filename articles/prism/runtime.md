# Prism Javascript Runtime Reference

Prism is a fast, flexible, and easy-to-use application for mocking and testing HTTP API's. To help improve API testing effectiveness and bypass limitations in the OpenAPI specification, Prism comes with a full ES5-compatible Javascript runtime capable of supercharging your API workflow.

Some example use cases for the Prism Javascript runtime include:

* Getting, setting, removing cookies on requests
* Manipulating HTTP request content, including slicing and dicing response bodies or manipulating headers
* Seeding your tests with randomized data that conforms to a regex

Anything that can be done in Javascript can now be done within a Scenario step.

## Execution State

Prism is an orchestration engine as much as it is a proxy and test runner. When we talk about execution state, we are talking about what is currently being orchestrated. Prism can orchestrate HTTP calls, Javascript programs, and other referenced scenarios.

## Javascript Specification

The Prism Javascript Runtime is compliant with the ECMAScript 5/5.1 specification, with full ECMAScript 6 support coming soon.

## Globals

### Lodash

[Lodash v4.17.4](https://lodash.com/) - It is always loaded in the runtime as `_`.

### Console

The console objects gives you access to the Scenario Collection Logs. Use it to debug your scenarios.

```js
/**
* Useful for logging out general messages.
*
* @param {Object[]} object - The objects to log.
*/
console.log(object [, object, ...]);
console.info(object [, object, ...]);

/**
* Useful for logging out warning messages.
*
* @param {Object[]} object - The objects to log as a warning.
*/
console.warn(object [, object, ...]);

/**
* Useful for logging out error messages.
*
* @param {Object[]} object - The objects to log as an error.
*/
console.error(object [, object, ...]);
```

### Base64

Base-64 to help with encoding and decoding strings of data.

```js
/**
 * Creates a base-64 encoded ASCII string from a string.
 *
 * @param {string} string - the string to base-64 encode.
 * @returns {string} string - the base-64 encoded string.
 */
Base64.encode(string);

/**
 * Decodes a string of data which has been encoded using base-64 encoding.
 *
 * @param {string} string - the base-64 encoded string to decode.
 * @returns {string} string - the original string.
 */
Base64.decode(string);
```

### Stoplight Object (SL)

#### Sleep

```js
/**
 * Sleep the current running Scenario step.
 *
 * @param {integer} ms - Time to sleep in milliseconds.
 */
SL.sleep(ms);
```

#### Validate

```js
/**
 * Validate that a given object conforms to a given contract (JSON Schema).
 *
 * @typedef {Object} Message
 * @property {string} error
 * @property {string} details
 *
 * @param {*} object - The object to validate.
 * @param {Object} contract - JSON Schema to validate object against.
 *
 * @returns {Message[]} - Array of validation errors, if validation passes then msgs will be empty.
 */
var msgs = SL.schema.validate(object, contract);
```

#### Generate

```js
/**
 * Generate random data based on a contract (JSON Schema).
 *
 * @param {Object} contract - JSON Schema to use for dynamic data generation.
 *
 * @returns {*} - Generated data.
 */
var data = SL.schema.generate(contract);
```

#### Find Operation

```js
/**
*
* This describes the Stoplight representation of an HTTP operation. It is loosely based on OAS 3. You can find more descriptions of some of the properties described below here: https://swagger.io/specification/#operationObject.
*
* @typedef {Object} Operation
* @property {string} method
* @property {string} path
* @property {array} [tags]
* @property {string} [summary]
* @property {string} [description]
* @property {array} [security] - As described here: https://swagger.io/specification/#securitySchemeObject. For OAS2, if the operation defines security requirements, we need to look up the security definition and inline it here. If it is for oauth, should include the scopes property from the original operation security property.
* @property {array} [servers]
* @property {Object} [params] - The path parameters. For OAS2, these are a combination of the parameters defined at the operation, AND at the operation's path (one level up from the operation in the spec).
* @property {Object} .schema - A JSON Schema.
* @property {Object} [.example] - Generate this from defaults set in OAS 2.0
* @property {Object} [query] - The query parameters. For OAS2, these are a combination of the query parameters defined at the operation, AND at the operation's path (one level up from the operation in the spec).
* @property {Object} .schema - A JSON Schema.
* @property {Object} [.example] - Generate this from defaults set in OAS 2.0
* @property {Object} [headers] - The header parameters. For OAS2, these are a combination of the header parameters defined at the operation, AND at the operation's path (one level up from the operation in the spec).
* @property {Object} .schema - A JSON Schema.
* @property {Object} [.example] - Generate this from defaults set in OAS 2.0
* @property {Object} [body]
* @property {string} [.description]
* @property {Object} [.content]
* @property {Object} [.[\w\/-]+] - Each key is usually a mime type (ie application/json), but can be any string.
For OAS 2.0, this should come from the consumes key.
* @property {Object} [.schema]
* @property {Object} [.examples]
* @property {Object} [.[\w\/-]+]
* @property {string} [.summary]
* @property {string} [.description]
* @property {string|Object} .value
* @property {Object} [responses]
* @property {Object} [.[\w\/-]+] - Each key is a response code or the string "default".
* @property {string} [.description]
* @property {Object} [.headers]
* @property {Object} [.schema]
* @property {Object} [.example]
* @property {Object} [.content]
* @property {Object} [.[\w\/-]+] - Each key is usually a mime type (ie application/json), but can be any string.
* @property {Object} [.schema]
* @property {Object} [.examples]
* @property {Object} [.[\w\/-]+]
* @property {string} [.summary]
* @property {string} [.description]
* @property {string|Object} .value
*
* @param {string} path - Request URL Path to search for in OAS connected Specification.
* @param {string} method - Reqeust method to search for in OAS connected Specfication.
*
* @returns {Operation} - Stoplight opeartion that matches given path and method.
*/
var operation = SL.specs.findOperation(path, method);
```

### Double Dollar - $$

The double dollar sign variable represents the currently running collection object.

#### Stop

```js
/**
 * Stops the current Scenario Collection run.
 */
$$.stop();
```

#### Environment

Current environment for a Scenario Collection Run.

#### Get / Set

```js
/**
 * Get all your environment variables.
 *
 * @returns {Object} - The current environment varibles.
 */
var env = $$.env.get();

/**
 * Get the value of an environment variable.
 *
 * @param {string} string - The path to an environment variables.
 *
 * @returns {(Object|undefined)} value - The value at the given path. If path isn't found then undefined is returned.
 */
var value = $$.env.get(string);

/**
 * Set all your environment variables.
 *
 * @param {Object} object - The value to replace your current environment variables with.
 */
$$.env.set(object);

/**
 * Set the value of an environment variable.
 *
 * @param {string} string - The path to set. Will try to create appropriate objects if path doesn't exist.
 * @param {Object} object - The value to set at the given path on your environment.
 */
$$.env.set(string, object);
```

#### Request

The request object on double dollar sign is a special object to help with Prism Instances. Anytime a request is sent through Prism and a Prism instance is being served, that incoming request will be parsed and set on the double dollar sign request method. Double Dollar Request is defined in Prism Conductor Instances, but it won't have any affect on the Scenario Collection run.

#### Get / Set

```js
/**
 * Get the whole request object.
 *
 * @typedef {name:string, value:string} Header
 *
 * @returns {Object} request - The current request coming into prism.
 * @returns {string} request.method
 * @returns {string} request.url
 * @returns {Object.<Header.name, Header.value>} request.headers
 * @returns {*} request.body
 */
var request = $$.request.get();

/**
 * Get a value on the request object at a given path.
 *
 * @param {string} string - The path to fetch on the request object.
 *
 * @returns {(Object|undefined)} - The value at the given path for the current Prism request. If path isn't found, then undefined is returned.
 */
var value = $$.request.get(string);

/**
 * Set the whole request object.
 *
 * @param {Object} request - Set the current request coming into Prism.
 * @param {string} request.method
 * @param {string} request.url
 * @param {Object.<Header>} request.headers
 * @param {*} request.body
 */
$$.request.set(request);

/**
 * Set a value on the request object at a given path.
 *
 * @param {string} string - The path to set on the request object. Will try to create appropriate objects along the path if it doesn't exist.
 * @param {Object} object - The object to set at given path.
 */
$$.request.set(string, object);
```

#### Method Get / Set

```js
/**
 * Get the current request's method.
 *
 * @returns {string} - The HTTP method for Double Dollar Sign request.
 */
var method = $$.request.method.get();

/**
 * Set the current request's method.
 *
 * @param {string} method - The new HTTP method for Double Dollar Sign request.
 */
$$.request.method.set(method);
```

#### URL Get / Set

```js
/**
 * Get the current request's url.
 *
 * @returns {string} - The HTTP url for Double Dollar Sign request.
 */
var url = $$.request.url.get();

/**
 * Set the current request's url.
 *
 * @param {string} url - The new url for Double Dollar Sign request.
 */
$$.request.url.set(url);
```

#### Path Get / Set

```js
/**
 * Get the current request's path.
 *
 * @returns {string} - The HTTP path for Double Dollar Sign request.
 */
var path = $$.request.path.get();

/**
 * Set the current request's path.
 *
 * @param {string} path - The new path for Double Dollar Sign request.
 */
$$.request.path.set(path);
```

#### Scheme Get / Set

```js
/**
 * Get the current request's scheme.
 *
 * @returns {string} - The HTTP scheme for Double Dollar Sign request.
 */
var scheme = $$.request.scheme.get();

/**
 * Set the current request's scheme.
 *
 * @param {string} scheme - The new scheme for Double Dollar Sign request.
 */
$$.request.scheme.set(scheme);
```

#### Host Get / Set

```js
/**
 * Get the current request's host.
 *
 * @returns {string} - The HTTP host for Double Dollar Sign request.
 */
var host = $$.request.host.get();

/**
 * Set the current request's host.
 *
 * @param {string} host - The new host for Double Dollar Sign request.
 */
$$.request.host.set(host);
```

#### Query Get / Set / Add / Del

```js
/**
 * Get the current request's query.
 *
 * @typedef {name:string, value:string} Query
 *
 * @returns {Object.<Query>} - The HTTP query object for Double Dollar Sign request.
 */
var query = $$.request.query.get();

/**
 * Get the current request's query.
 *
 * @param {string} key - The key of the query value to get.
 *
 * @returns {string} - The HTTP query value at the given key for Double Dollar Sign request.
 */
var value = $$.request.query.get(key);

/**
 * Set the current request's query.
 *
 * @typedef {name:string, value:string} Query
 *
 * @param {Object.<Query>} query - The new HTTP query object for Double Dollar Sign request.
 */
$$.request.query.set(query);

/**
 * Set the current request's query.
 *
 * @param {string} key - The key of the query value to set.
 * @param {string} value - The HTTP query value to set at the given key.
 */
$$.request.query.set(key, value);

/**
 * Add the give value to the current key. If key isn't defined behaves like $$.request.query.set.
 *
 * @param {string} key - The key of the query value to add to.
 * @param {string} value - The HTTP query value to add at the given key.
 */
$$.request.query.add(key, value);

/**
 * Del the current request's query at key.
 *
 * @param {string} key - The key to delete on the query string.
 */
$$.request.query.del(key);
```

#### Headers Get / Set / Add / Del

```js
/**
 * Get the current request's headers.
 *
 * @typedef {name:string, value:string} Header
 *
 * @returns {Object.<Header>} - The HTTP headers object for Double Dollar Sign request.
 */
var headers = $$.request.headers.get();

/**
 * Get the current request's headers.
 *
 * @param {string} key - The key of the headers value to get.
 *
 * @returns {string} - The HTTP headers value at the given key for Double Dollar Sign request.
 */
var value = $$.request.headers.get(key);

/**
 * Set the current request's headers.
 *
 * @typedef {name:string, value:string} Header
 *
 * @param {Object.<Header>} headers - The new HTTP headers object for Double Dollar Sign request.
 */
$$.request.headers.set(headers);

/**
 * Set the current request's headers.
 *
 * @param {string} key - The key of the headers value to set.
 * @param {string} value - The HTTP headers value to set at the given key.
 */
$$.request.headers.set(key, value);

/**
 * Add the give value to the current key. If key isn't defined behaves like $$.request.headers.set.
 *
 * @param {string} key - The key of the headers value to add to.
 * @param {string} value - The HTTP headers value to add at the given key.
 */
$$.request.headers.add(key, value);

/**
 * Del the current request's headers at key.
 *
 * @param {string} key - The key to delete on the headers string.
 */
$$.request.headers.del(key);
```

#### Content Type / Content Negotiation

```js
/**
 * Parses the Accept header and returns an ordered list of mime types that the client will accept.
 *
 * @returns {string[]} - The types that the request accepts, in the order of the client's preference (most preferred first).
 */
var accepts = $$.request.accepts.contentTypes.get();
```

#### Cookies Get / Set

```js
/**
 * Get all HTTP Cookies on request.
 *
 * @typedef {Object} Cookie
 * @property {string} value
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @returns {Object.<name:string, Cookie>} - A map of cookies on $$.request.
 */
var cookies = $$.request.cookies.get();

/**
 * Get the HTTP Cookie at given name on the current request.
 *
 * @typedef {Object} Cookie
 * @property {string} value
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @param {string} name - The name of the HTTP Cookie to get.
 *
 * @returns {(Cookie|undefinded)} - The HTTP Cookie for the given name. If the cookie doesn't exist then cookie will be undefined.
 */
var cookie = $$.request.cookies.get(name);

/**
 * Set all HTTP Cookies on request.
 *
 * @typedef {Object} Cookie
 * @property {string} value
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @param {Object.<name:string, Cookie>} cookies - A map of new cookies to set on $$.request.
 */
$$.request.cookies.set(cookies);

/**
 * Set HTTP Cookie on request.
 *
 * @param {string} name - The name of the cookie to set.
 * @param {string} value - The value of the cookie to set.
 */
$$.request.cookies.set(name, value);

/**
 * Set HTTP Cookie on request.
 *
 * @typedef {Object} Options
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @param {string} name - The name of the cookie to set.
 * @param {string} value - The value of the cookie to set.
 * @param {Options} [options] - Additional values to set on the cookie.
 */
$$.request.cookies.set(name, value, options);
```

#### Body Get / Set

```js
/**
 *  Get the current request body.
 *
 * @returns {*} - The current request body, if there is no body on the equest then undefined is returned.
 */
var body = $$.request.body.get();

/**
 * Get the value on the current request body at the given path.
 *
 * @param {string} path - Path is the location of the value to return from the current request body.
 *
 * @returns {*} - The value at the given path on the request body. If the value doesn't exist then undefined is returned.
 */
var value = $$.request.body.get(path);

/**
 * Set the current request body.
 *
 * @param {*} body - The new request body to set.
 */
$$.request.body.set(body);

/**
 * Set the value at the given path on the current request body.
 *
 * @param {string} path - Path is the location of the value to set on the current request. If path doesn't exist then try to create it.
 * @param {*} value - The value to set at the given path.
 */
$$.request.body.set(path, value);
```

#### Response

Double dollar response is what is returned by Prism.

#### Get / Set

```js
/**
 * Get the whole response object.
 *
 * @typedef {name:string, value:string} Header
 *
 * @typedef {Object} Response
 * @property {integer} status
 * @property {integer} time
 * @property {Object.<Header>} headers
 * @property {*} body
 *
 * @returns {Response} - The current response object.
 */
var response = $$.response.get();

/**
 * Get a value on the response object at a given path.
 *
 * @param {string} string - The path to fetch on the response object.
 *
 * @returns {*} - The current value at the path on the response. If path isn't found, then undefined is returned.
 */
var value = $$.response.get(string);

/**
 * Set the whole response object.
 *
 * @typedef {name:string, value:string} Header
 *
 * @typedef {Object} Response
 * @property {integer} status
 * @property {Object.<Header>} headers
 * @property {*} body
 *
 * @param {Resposne} response  - Set the current response object.
 */
$$.response.set(response);

/**
 * Set a value on the response object at a given path.
 *
 * @param {string} string - The path to set on the response object. Will try to create appropriate objects at path if it doesn't exist.
 * @param {*} object - The object to set at given path.
 */
$$.response.set(string, object);
```

#### Status Code Get / Set

```js
/**
 * Get the current response's status code.
 *
 * @returns {integer} - The HTTP status code for the current response.
 */
var status = $$.response.status.get();

/**
 * Set the current response's status code.
 *
 * @param {integer} status - The new HTTP status code for the current response.
 */
$$.response.status.set(status);
```

#### Time Get

```js
/**
 * Get round trip time.
 *
 * @returns {integer} - The time it took for the current reqeust to respond in milliseconds.
 */
var roundTrip = $$.response.time.get();
```

#### Headers Get / Set / Add / Del

```js
/**
 * Get the current response's headers.
 *
 * @typedef {name:string, value:string} Header
 *
 * @returns {Object.<Header>} - The HTTP headers object for the current response.
 */
var headers = $$.response.headers.get();

/**
 * Get the current response's headers.
 *
 * @param {string} key - The key of the headers value to get.
 *
 * @returns {string} - The HTTP headers value at the given key for the current response.
 */
var value = $$.response.headers.get(key);

/**
 * Set the current response's headers.
 *
 * @typedef {name:string, value:string} Header
 *
 * @param {Object.<Header>} - The new HTTP headers object for the current response.
 */
$$.response.headers.set(headers);

/**
 * Set the current response's headers.
 *
 * @param {string} key - The key of the headers value to set.
 * @param {string} value - The HTTP headers value to set at the given key.
 */
$$.response.headers.set(key, value);

/**
 * Add the give value to the current key. If key isn't defined behaves like $$.response.headers.set.
 *
 * @param {string} key - The key of the headers value to add to.
 * @param {string} value - The HTTP headers value to add at the given key.
 */
$$.response.headers.add(key, value);

/**
 * Del the current response's headers at key.
 *
 * @param {string} key - The key to delete on the headers string.
 */
$$.response.headers.del(key);
```

#### Cookies Get / Set

```js
/**
 * Get all HTTP Cookies on response.
 *
 * @typedef {Object} Cookie
 * @property {string} value
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @returns {Object.<name:string, Cookie>} - A map of cookies on $$.response.
 */
var cookies = $$.response.cookies.get();

/**
 * Get the HTTP Cookie at given name on the current response.
 *
 * @typedef {Object} Cookie
 * @property {string} value
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @param {string} name - The name of the HTTP Cookie to get.
 *
 * @returns {(Cookie|undefined)} - The HTTP Cookie for the given name. If the cookie doesn't exist then cookie will be undefined.
 */
var cookie = $$.response.cookies.get(name);

/**
 * Set all HTTP Cookies on response.
 *
 * @typedef {Object} Cookie
 * @property {string} value
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @param {Object.<name:string, Cookie>} cookies - A map of new cookies to set on $$.response.
 */
$$.response.cookies.set(cookies);

/**
 * Set HTTP Cookie on response.
 *
 * @param {string} name - The name of the cookie to set.
 * @param {string} value - The value of the cookie to set.
 */
$$.response.cookies.set(name, value);

/**
 * Set HTTP Cookie on response.
 *
 * @typedef {Object} Options
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @param {string} name - The name of the cookie to set.
 * @param {string} value - The value of the cookie to set.
 * @param {Options} [options] - Additional values to set on the cookie.
 */
$$.response.cookies.set(name, value, options);
```

#### Body Get / Set

```js
/**
 * Get the current response body.
 *
 * @returns {*} - The current response body, if there is no body on the response then undefined is returned.
 */
var body = $$.response.body.get();

/**
 * Get the value on the current response body at the given path.
 *
 * @param {string} path - Path is the location of the value to return from the current response body.
 *
 * @returns {*} - The value at the given path on the response body. If the value doesn't exist then undefined is returned.
 */
var value = $$.response.body.get(path);

/**
 * Set the current response body.
 *
 * @param {*} body - The new response body to set.
 */
$$.response.body.set(body);

/**
 * Set the value at the given path on the current response body.
 *
 * @param {string} path - Path is the location of the value to set on the current response. If path doesn't exist then try to create it.
 * @param {*} value - The value to set at the given path.
 */
$$.response.body.set(path, value);
```

# Dollar Sign - $

#### Context

Each scenario in your collection has it's own set of context variables. Context is especially useful for passing data between steps in a scenario.

#### Get / Set

```js
/**
 * Get all your context variables.
 *
 * @returns {Object} - The current context varibles.
 */
var ctx = $.ctx.get();

/**
 * Get the value of an context variable.
 *
 * @param {string} string - The path to an context variables.
 *
 * @returns {(Object|undefined)} value - The value at the given path. If path isn't found then undefined is returned.
 */
var value = $.ctx.get(string);

/**
 * Set all your context variables.
 *
 * @param {Object} object - The value to replace your current context variables with.
 */
$.ctx.set(object);

/**
 * Set the value of an context variable.
 *
 * @param {string} string - The path to set. Will try to create appropriate objects if path doesn't exist.
 * @param {Object} object - The value to set at the given path on your context.
 */
$.ctx.set(string, object);
```

#### Stop

```js
/**
 * Stops the current Scenario run.
 */
$.stop();
```

# Steps

#### Stop

```js
/**
 * Stops the current Step.
 */
stop();
```

#### Tests

The test object is useful for when you need a litt bit more power. For example you need to loop over an object, check to see if a property exists and if it does assert that is greater than 1.

```js
/**
 * Tests is just a global object in the runtime, the key's are a message and the value is a boolean.
 */

// Example
var body = $$.request.body.get();
var count = 0;
_.forEach(body, function(value, key) {
  if (key === "foo") {
    tests["[Count " + count + "] foo should be greater than one"] = value > 1;
    count++;
  }
});
```

## HTTP

#### Step Request

#### Get / Set

```js
/**
 * Get the whole request object.
 *
 * @typedef {name:string, value:string} Header
 *
 * @returns {Object} request - The current request for a Scenario step.
 * @returns {string} request.method
 * @returns {string} request.url
 * @returns {Object.<Header.name, Header.value>} request.headers
 * @returns {*} request.body
 */
var request = input.get();

/**
 * Get a value on the request object at a given path.
 *
 * @param {string} string - The path to fetch on the request object.
 *
 * @returns {(Object|undefined)} - The value at given path for the current Scenario step request.  If path isn't found, then undefined is returned.
 */
var value = input.get(string);

/**
 * Set the whole request object.
 *
 *   object ({
 *     method: string,
 *     url: string,
 *     headers: {
 *       key: value,
 *     },
 *     body: object
 *   }) - Set the current Scneario step request.
 */
input.set(object);

/**
 * Set a value on the request object at a given path.
 *
 * @param {string} string - The path to set on the request current Scenario step. Will try to create appropriate objects along the path if it doesn't exist.
 * @param {Object} object - The object to set at given path.
 */
input.set(string, object);
```

#### Method Get / Set

```js
/**
 * Get the current request's method.
 *
 * @returns {string} method - The HTTP method for the current Scenario step request.
 */
var method = input.method.get();

/**
 * Set the current request's method.
 *
 * @param {string} method  - The new HTTP method for the current Scenario step request.
 */
input.method.set(method);
```

#### URL Get / Set

```js
/**
 * Get the current request's url.
 *
 * @returns {string} url - The HTTP url for the current Scenario step request.
 */
var url = input.url.get();

/**
 * Set the current request's url.
 *
 * @param {string} url - The new url for the current Scenario step request.
 */
input.url.set(url);
```

#### Path Get / Set

```js
/**
 * Get the current request's path.
 *
 * @returns {string} - The HTTP path for the current Scenario Step request.
 */
var path = input.path.get();

/**
 * Set the current request's path.
 *
 * @param {string} path - The new path for the current Scenario Step request.
 */
input.path.set(path);
```

#### Scheme Get / Set

```js
/**
 * Get the current request's scheme.
 *
 * @returns {string} - The HTTP scheme for the current Scenario Step request.
 */
var scheme = input.scheme.get();

/**
 * Set the current request's scheme.
 *
 * @param {string} scheme - The new scheme for the current Scenario Step request.
 */
input.scheme.set(scheme);
```

#### Host Get / Set

```js
/**
 * Get the current request's host.
 *
 * @returns {string} - The HTTP host for the current Scenario Step request.
 */
var host = input.host.get();

/**
 * Set the current request's host.
 *
 * @param {string} host - The new host for the current Scenario Step request.
 */
input.host.set(host);
```

#### Query Get / Set / Add / Del

```js
/**
 * Get the current request's query.
 *
 * @typedef {name:string, value:string} Query
 *
 * @returns {Object.<Query>} - The HTTP query object for the current Scenario Step request.
 */
var query = input.query.get();

/**
 * Get the current request's query.
 *
 * @param {string} key - The key of the query value to get.
 *
 * @returns {string} - The HTTP query value at the given key for the current Scenario Step request.
 */
var value = input.query.get(key);

/**
 * Set the current request's query.
 *
 * @typedef {name:string, value:string} Query
 *
 * @param {Object.<Query>} query - The new HTTP query object for the current Scenario Step request.
 */
input.query.set(query);

/**
 * Set the current request's query.
 *
 * @param {string} key - The key of the query value to set.
 * @param {string} value - The HTTP query value to set at the given key.
 */
input.query.set(key, value);

/**
 * Add the give value to the current key. If key isn't defined behaves like input.query.set.
 *
 * @param {string} key - The key of the query value to add to.
 * @param {string} value - The HTTP query value to add at the given key.
 */
input.query.add(key, value);

/**
 * Del the current request's query at key.
 *
 * @param {string} key - The key to delete on the query string.
 */
input.query.del(key);
```

#### Headers Get / Set / Add / Del

```js
/**
 * Get the current request's headers.
 *
 * @typedef {name:string, value:string} Header
 *
 * @returns {Object.<Header>} - The HTTP headers object for the current Scenario Step request.
 */
var headers = input.headers.get();

/**
 * Get the current request's headers.
 *
 * @param {string} key - The key of the headers value to get.
 *
 * @returns {string} - The HTTP headers value at the given key for the current Scenario Step request.
 */
var value = input.headers.get(key);

/**
 * Set the current request's headers.
 *
 * @typedef {name:string, value:string} Header
 *
 * @param {Object.<Header>} headers - The new HTTP headers object for the current Scenario Step request.
 */
input.headers.set(headers);

/**
 * Set the current request's headers.
 *
 * @param {string} key - The key of the headers value to set.
 * @param {string} value - The HTTP headers value to set at the given key.
 */
input.headers.set(key, value);

/**
 * Add the give value to the current key. If key isn't defined behaves like input.headers.set.
 *
 * @param {string} key - The key of the headers value to add to.
 * @param {string} value - The HTTP headers value to add at the given key.
 */
input.headers.add(key, value);

/**
 * Del the current request's headers at key.
 *
 * @param {string} key - The key to delete on the headers string.
 */
input.headers.del(key);
```

#### Content Types Content Negotiation

```js
/**
 * Parses the Accept header and returns an ordered list of mime types that the client will accept.
 *
 * @returns {string[]} - The types that the request accepts, in the order of the client's preference (most preferred first).
 */
var accepts = input.accepts.contentTypes.get();
```

#### Cookies Get / Set

```js
/**
 * Get all HTTP Cookies on request.
 *
 * @typedef {Object} Cookie
 * @property {string} value
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @returns {Object.<name:string, Cookie>} - A map of cookies on the current Scenario Step request.
 */
var cookies = input.cookies.get();

/**
 * Get the HTTP Cookie at given name on the current request.
 *
 * @typedef {Object} Cookie
 * @property {string} value
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @param {string} name - The name of the HTTP Cookie to get.
 *
 * @returns {(Cookie|undefinded)} - The HTTP Cookie for the given name. If the cookie doesn't exist then cookie will be undefined.
 */
var cookie = input.cookies.get(name);

/**
 * Set all HTTP Cookies on request.
 *
 * @typedef {Object} Cookie
 * @property {string} value
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @param {Object.<name:string, Cookie>} cookies - A map of new cookies to set on input.
 */
input.cookies.set(cookies);

/**
 * Set HTTP Cookie on request.
 *
 * @param {string} key - The name of the cookie to set.
 * @param {string} value - The value of the cookie to set.
 */
input.cookies.set(name, value);

/**
 * Set HTTP Cookie on request.
 *
 * @typedef {Object} Options
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @param {string} name - The name of the cookie to set.
 * @param {string} value - The value of the cookie to set.
 * @param {Options} [options] - Additional values to set on the cookie.
 */
input.cookies.set(name, value, options);
```

#### Body Get / Set

```js
/**
 * Get the current request body.
 *
 * @returns {*} - The current Scenario Step request body, if there is no body on the request then undefined is returned.
 */
var body = input.body.get();

/**
 * Get the value on the current request body at the given path.
 *
 * @param {string} path - Path is the location of the value to return from the current request body.
 *
 * @returns {*} - The value at the given path on the request body. If the value doesn't exist then undefined is returned.
 */
var value = input.body.get(path);

/**
 * Set the current request body.
 *
 * @param {*} body - The new request body to set.
 */
input.body.set(body);

/**
 * Set the value at the given path on the current request body.
 *
 * @param {string} path - Path is the location of the value to set on the current request. If path doesn't exist then try to create it.
 * @param {*} value  - The value to set at the given path.
 */
input.body.set(path, value);
```

#### Step Response

#### Get / Set

```js
/**
 * Get the whole response object.
 *
 * @typedef {name:string, value:string} Header
 *
 * @typedef {Object} Response
 * @property {integer} status
 * @property {integer} time
 * @property {Object.<Header>} headers
 * @property {*} body
 *
 * @returns {Response} - The current response object.
 */
var response = output.get();

/**
 * Get a value on the response object at a given path.
 *
 * @param {string} string - The path to fetch on the response object.
 *
 * @returns {*} - The current value at the path on the response. If path isn't found, then undefined is returned.
 */
var value = output.get(string);

/**
 * Set the whole response object.
 *
 * @typedef {Object} Response
 * @property {integer} status
 * @property {Object.<Header>} headers
 * @property {*} body
 *
 * @param {Resposne} response - Set the current response object.
 */
output.set(object);

/**
 * Set a value on the response object at a given path.
 *
 * @param {string} string - The path to set on the response object. Will try to create appropriate objects at path if it doesn't exist.
 * @param {*} object - The object to set at given path.
 */
output.set(string, object);
```

#### Status Code Get / Set

```js
/**
 * Get the current response's status code.
 *
 * @returns {integer} - The HTTP status code for the current response.
 */
var status = output.status.get();

/**
 * Set the current response's status code.
 *
 * @param {integer} status - The new HTTP status code for the current response.
 */
output.status.set(status);
```

#### Time Get

```js
/**
 * Get round trip time.
 *
 * @returns {integer} - The time it took for the current reqeust to respond in milliseconds.
 */
var roundTrip = output.time.get();
```

#### Headers Get / Set / Add / Del

```js
/**
 * Get the current response's headers.
 *
 * @typedef {name:string, value:string} Header
 *
 * @returns {Object.<Header>} - The HTTP headers object for the current response.
 */
var headers = output.headers.get();

/**
 * Get the current response's headers.
 *
 * @param {string} key - The key of the headers value to get.
 *
 * @returns {string} - The HTTP headers value at the given key for the current response.
 */
var value = output.headers.get(key);

/**
 * Set the current response's headers.
 *
 * @typedef {name:string, value:string} Header
 *
 * @param {Object.<Header>} - The new HTTP headers object for the current response.
 */
output.headers.set(headers);

/**
 * Set the current response's headers.
 *
 * @param {string} key - The key of the headers value to set.
 * @param {string} value - The HTTP headers value to set at the given key.
 */
output.headers.set(key, value);

/**
 * Add the give value to the current key. If key isn't defined behaves like output.headers.set.
 *
 * @param {string} key - The key of the headers value to add to.
 * @param {string} value - The HTTP headers value to add at the given key.
 */
output.headers.add(key, value);

/**
 * Del the current response's headers at key.
 *
 * @param {string} key - The key to delete on the headers string.
 */
output.headers.del(key);
```

#### Cookies Get / Set

```js
/**
 * Get all HTTP Cookies on response.
 *
 * @typedef {Object} Cookie
 * @property {string} value
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @returns {Object.<name:string, Cookie>} - A map of cookies on output.
 */
var cookies = output.cookies.get();

/**
 * Get the HTTP Cookie at given name on the current response.
 *
 * @typedef {Object} Cookie
 * @property {string} value
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @param {string} name - The name of the HTTP Cookie to get.
 *
 * @returns {(Cookie|undefined)} - The HTTP Cookie for the given name. If the cookie doesn't exist then cookie will be undefined.
 */
var cookie = output.cookies.get(name);

/**
 * Set all HTTP Cookies on response.
 *
 * @typedef {Object} Cookie
 * @property {string} value
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @param {Object.<name:string, Cookie>} cookies - A map of new cookies to set on output.
 */
output.cookies.set(cookies);

/**
 * Set HTTP Cookie on response.
 *
 * @param {string} name - The name of the cookie to set.
 * @param {string} value - The value of the cookie to set.
 */
output.cookies.set(name, value);

/**
 * Set HTTP Cookie on response.
 *
 * @typedef {Object} Options
 * @property {string} path
 * @property {string} domain
 * @property {date} expires
 * @property {boolean} secure
 * @property {boolean} httponly
 * @property {integer} maxage
 *
 * @param {string} name - The name of the cookie to set.
 * @param {string} value - The value of the cookie to set.
 * @param {Options} [options] - Additional values to set on the cookie.
 */
output.cookies.set(name, value, options);
```

#### Body Get / Set

```js
/**
 * Get the current response body.
 *
 * Returns
 * @returns {*} - The current response body, if there is no body on the response then undefined is returned.
 */
var body = output.body.get();

/**
 * Get the value on the current response body at the given path.
 *
 * @param {string} path - Path is the location of the value to return from the current response body.
 *
 * @returns {*} - The value at the given path on the response body. If the value doesn't exist then undefined is returned.
 */
var value = output.body.get(path);

/**
 * Set the current response body.
 *
 * @param {*} body - The new response body to set.
 */
output.body.set(body);

/**
 * Set the value at the given path on the current response body.
 *
 * @param {string} path - Path is the location of the value to set on the current response. If path doesn't exist then try to create it.
 * @param {*} value - The value to set at the given path.
 */
output.body.set(path, value);
```
