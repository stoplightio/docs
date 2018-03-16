# Introduction

Prism is really good at mocking and testing APIs. It is fast, flexible and easy to use. The scenarios and oas specifications have their limits, which is why Prism has a Javascript Runtime. Most of the time you won't need to jump into the runtime, and you should ask yourself before doing so if you have too use it. The runtime is powerful, and we chose javascript because of its flexibility and familiarity. It is perfect if you need to get/set/add/del(/eat?) cookies, loop over a http response body or seed your tests with some data.

## Execution State

The current state of prism dictates what is made available in the runtime. At the end of the day, Prism isn't really a proxy or a test runner. It is an orchestration engine, so when we are talking about state, we are talking about what is currently being orchestrated. Today Prism can orchestrate http, javascript and reffed scenarios.

## Execution Order of Scenario Steps

### HTTP

### Scripts

### Refs

# Javascript Specification

EMacs 5/5.1

Full ES 6 comming soon.

# Globals

#### Lodash

[Lodash v4.17.4](https://lodash.com/) - It is always loaded in the runtime as `_`.

#### Console

The console objects gives you access to the Scenario Collection Logs. Use it to debug your sceanrios.

```js
/*
    Useful for logging out general messages.

    Arguments
      object [, object, ...] - The objects to log.
*/
console.log(object [, object, ...]);
console.info(object [, object, ...]);

/*
    Useful for logging out warning messages.

    Arguments
      object [, object, ...] - The objects to log as a warning.
*/
console.warn(object [, object, ...]);

/*
    Useful for logging out error messages.

    Arguments
      object [, object, ...] - The objects to log as an error.
*/
console.error(object [, object, ...]);
```

#### Base64

Base-64 to help with encoding and decoding strings of data.

```js
/*
    Creates a base-64 encoded ASCII string from a string.

    Arguments
      string - the string to base-64 encode.

    Returns
      string - the base-64 encoded string.
*/
Base64.encode(string);

/*
    Decodes a string of data which has been encoded using base-64 encoding.

    Arguments
      string - the base-64 encoded string to decode.

    Returns
      string - the original string.
*/
Base64.decode(string);
```

# Stoplight

```js
/*

*/
SL.sleep => function(ms)
```

```js
/*

*/
SL.schema.validate => function(object, schema)
```

```js
/*

*/
SL.schema.generate => function(schema)
```

```js
/*

*/
// TODO: Support default responses
// TODO: Check to see if options is hooked up
// TODO: If hooked up document it.
// Returns HTTPOperation -> https://next.stoplight.io/stoplight/hubs-spec#/definitions/HTTP_Operation
SL.specs.findOperation => function(path, method, options)
```

# Double Dollar - $$

Double Dollar sign is the collection object.

##### Stop

```js
/*
    Stops the current Scenario Collection run.
*/
$$.stop();
```

#### Environment

Current environment for a Scenario Collection Run.

##### Get / Set

```js
/*
    Get all your environment variables.

    Returns
      object - The current environment varibles.
*/
var env = $$.env.get();

/*
    Get the value of an environment variable.

    Arguments
      string - The path to an environment variables.

    Returns
      value (object) | undefined - The value at the given path. If path isn't found then undefined is returned.
*/
var value = $$.env.get(string);

/*
    Set all your environment variables.

    Arguments
      object - The value to replace your current environment variables with.
*/
$$.env.set(object);

/*
    Set the value of an environment variable.

    Arguments
      string - The path to set. Will try to create appropriate objects if path doesn't exist.
      object - The value to set at the given path on your environment.
*/
$$.env.set(string, object);
```

#### Request

The request object on double dollar sign is a special object to help with Prism Instances. Anytime a request is sent through prism and a prism instance is being served, that incoming request will be parsed and set on the double dollar sign request method. Double Dollar Request is defined in Prism Conductor Instances, but it won't have any affect on the Scenario Collection run.

##### Get / Set

```js
/*
    Get the whole request object.

    Returns
      object ({
        method: string,
        url: string,
        headers: {
          key: value,
        },
        body: object
      }) - The current request coming into prism.
*/
var request = $$.request.get();

/*
    Get a value on the request object at a given path.

    Arguments
      string - The path to fetch on the request object.

    Returns
     value (object) | undefined - The current request coming into prism. If path isn't found, then undefined is returned.
*/
var value = $$.request.get(string);

/*
    Set the whole request object.

    Arguments
      object ({
        method: string,
        url: string,
        headers: {
          key: value,
        },
        body: object
      }) - Set the current request coming into Prism.
*/
$$.request.set(object);

/*
    Set a value on the request object at a given path.

    Arguments
      string - The path to set on the request object. Will try to create appropriate
      object - The object to set at given path.
*/
$$.request.set(string, object);
```

##### Method Get / Set

```js
/*
    Get the current request's method.

    Returns
      method (string) - The HTTP method for Double Dollar Sign Request.
*/
var method = $$.request.method.get();

/*
    Set the current request's method.

    Arguments
      method (string) - The new HTTP method for Double Dollar Sign Request.
*/
$$.request.method.set(method);
```

##### URL Get / Set

```js
/*
    Get the current request's url.

    Returns
      url (string) - The HTTP url for Double Dollar Sign Request.
*/
var url = $$.request.url.get();

/*
    Set the current request's url.

    Arguments
      url (string) - The new url for Double Dollar Sign Request.
*/
$$.request.url.set(url);
```

##### Path Get / Set

```js
/*
    Get the current request's path.

    Returns
      path (string) - The HTTP path for Double Dollar Sign Request.
*/
var path = $$.request.path.get();

/*
    Set the current request's path.

    Arguments
      path (string) - The new path for Double Dollar Sign Request.
*/
$$.request.path.set(path);
```

##### Scheme Get / Set

```js
/*
    Get the current request's scheme.

    Returns
      scheme (string) - The HTTP scheme for Double Dollar Sign Request.
*/
var scheme = $$.request.scheme.get();

/*
    Set the current request's scheme.

    Arguments
      scheme (string) - The new scheme for Double Dollar Sign Request.
*/
$$.request.scheme.set(scheme);
```

##### Host Get / Set

```js
/*
    Get the current request's host.

    Returns
      host (string) - The HTTP host for Double Dollar Sign Request.
*/
var host = $$.request.host.get();

/*
    Set the current request's host.

    Arguments
      host (string) - The new host for Double Dollar Sign Request.
*/
$$.request.host.set(host);
```

##### Query Get / Set / Add / Del

```js
/*
    Get the current request's query.

    Returns
      query ({
        key: value
      }) - The HTTP query object for Double Dollar Sign Request.
*/
var query = $$.request.query.get();

/*
    Get the current request's query.

    Arguments
      key (string) - The key of the query value to get.

    Returns
      value (string) - The HTTP query value at the given key for Double Dollar Sign Request.
*/
var value = $$.request.query.get(key);

/*
    Set the current request's query.

    Returns
      query ({
        key: value
      }) - The new HTTP query object for Double Dollar Sign Request.
*/
$$.request.query.set(query);

/*
    Set the current request's query.

    Arguments
      key (string) - The key of the query value to set.
      value (string) - The HTTP query value to set at the given key.
*/
$$.request.query.set(key, value);

/*
    Add the give value to the current key. If key isn't defined behaves like $$.request.query.set.

    Arguments
      key (string) - The key of the query value to add to.
      value (string) - The HTTP query value to add at the given key.
*/
$$.request.query.add(key, value);

/*
    Del the current request's query at key.

    Arguments
      key (string) - The key to delete on the query string.
*/
$$.request.query.del(key);
```

##### Headers Get / Set / Add / Del

```js
/*
    Get the current request's headers.

    Returns
      headers ({
        key: value
      }) - The HTTP headers object for Double Dollar Sign Request.
*/
var headers = $$.request.headers.get();

/*
    Get the current request's headers.

    Arguments
      key (string) - The key of the headers value to get.

    Returns
      value (string) - The HTTP headers value at the given key for Double Dollar Sign Request.
*/
var value = $$.request.headers.get(key);

/*
    Set the current request's headers.

    Returns
      headers ({
        key: value
      }) - The new HTTP headers object for Double Dollar Sign Request.
*/
$$.request.headers.set(headers);

/*
    Set the current request's headers.

    Arguments
      key (string) - The key of the headers value to set.
      value (string) - The HTTP headers value to set at the given key.
*/
$$.request.headers.set(key, value);

/*
    Add the give value to the current key. If key isn't defined behaves like $$.request.headers.set.

    Arguments
      key (string) - The key of the headers value to add to.
      value (string) - The HTTP headers value to add at the given key.
*/
$$.request.headers.add(key, value);

/*
    Del the current request's headers at key.

    Arguments
      key (string) - The key to delete on the headers string.
*/
$$.request.headers.del(key);
```

##### Content Types Content Negotiation

```js
/*
    Parses the Accept header and returns an ordered list of mime types that the client will accept.

    Returns
      accepts ([string]) - The types that the request accepts, in the order of the client's preference (most preferred first).
*/
var accepts = $$.request.accepts.contentTypes.get();
```

##### Cookies Get / Set

```js
/*
    Get all HTTP Cookies on request.

    Returns
      cookies ({
        name: {
          value: string,
          path: string,
          domain: string,
          expires: date,
          secure: bool,
          httponly: bool,
          maxage: int
        }
      }) - A map of cookies on $$.request.
*/
var cookies = $$.request.cookies.get();

/*
    Get the HTTP Cookie at given name on the current request.

    Arguments
      name (string) - The name of the HTTP Cookie to get.

    Returns
      cookie ({
        value: string,
        path: string,
        domain: string,
        expires: date,
        secure: bool,
        httponly: bool,
        maxage: int
      }) | undefined - The HTTP Cookie for the given name. If the cookie doesn't exist then cookie will be undefined.
*/
var cookie = $$.request.cookies.get(name);

/*
    Set all HTTP Cookies on request.

    Arguments
      cookies ({
        name: {
          value: string,
          path: string,
          domain: string,
          expires: date,
          secure: bool,
          httponly: bool,
          maxage: int
        }
      }) - A map of new cookies to set on $$.request.
*/
$$.request.cookies.set(cookies);

/*
    Set HTTP Cookie on request.

    Arguments
      name (string) - The name of the cookie to set.
      value (string) - The value of the cookie to set.
*/
$$.request.cookies.set(name, value);

/*
    Set HTTP Cookie on request.

    Arguments
      name (string) - The name of the cookie to set.
      value (string) - The value of the cookie to set.
      options ({
        path: string,
        domain: string,
        expires: date,
        secure: bool,
        httponly: bool,
        maxage: int
      }) - Additional values to set on the cookie.
*/
$$.request.cookies.set(name, value, options);
```

##### Body Get / Set

```js
/*
    Get the current request body.

    Returns
      body (object) | undefined - The current request body, if there is no body on the request then undefined is returned.
*/
var body = $$.request.body.get();

/*
    Get the value on the current request body at the given path.

    Arguments
      path (string) - Path is the location of the value to return from the current request body.

    Returns
      value (object) | undefined - The value at the given path on the request body. If the value doesn't exist then undefined is returned.
*/
var value = $$.request.body.get(path);

/*
    Set the current request body.

    Arguments
      body (object) - The new request body to set.
*/
$$.request.body.set(body);

/*
    Set the value at the given path on the current request body.

    Arguments
      path (string) - Path is the location of the value to set on the current request. If path doesn't exist then try to create it.
      value (object) - The value to set at the given path.
*/
$$.request.body.set(path, value);
```

#### Response

TODO: Description. What does it mean for the conductor and prism instances.

##### Get / Set

```js
/*
    Get the whole response object.

    Returns
      object ({
        status: int,
        time: int,
        headers: {
          key: value,
        },
        body: object
      }) - The current response object.
*/
var response = $$.response.get();

/*
    Get a value on the response object at a given path.

    Arguments
      string - The path to fetch on the response object.

    Returns
     value (object) | undefined - The current value at the path on the response. If path isn't found, then undefined is returned.
*/
var value = $$.response.get(string);

/*
    Set the whole response object.

    Arguments
      object ({
        status: int,
        headers: {
          key: value,
        },
        body: object
      }) - Set the current response object.
*/
$$.response.set(object);

/*
    Set a value on the response object at a given path.

    Arguments
      string - The path to set on the response object. Will try to create appropriate objects at path if it doesn't exist.
      object - The object to set at given path.
*/
$$.response.set(string, object);
```

##### Status Code Get / Set

```js
/*
    Get the current response's status code.

    Returns
      status (int) - The HTTP status code for the current response.
*/
var status = $$.response.status.get();

/*
    Set the current response's status code.

    Arguments
      status (int) - The new HTTP status code for the current response.
*/
$$.response.status.set(status);
```

##### Time Get

```js
/*
    Get round trip time.

    Returns
      roundTrip (int) - The time it took for the current reqeust to respond in milliseconds.
*/
var roundTrip = $$.response.time.get();
```

##### Headers Get / Set / Add / Del

```js
/*
    Get the current response's headers.

    Returns
      headers ({
        key: value
      }) - The HTTP headers object for the current response.
*/
var headers = $$.response.headers.get();

/*
    Get the current response's headers.

    Arguments
      key (string) - The key of the headers value to get.

    Returns
      value (string) - The HTTP headers value at the given key for the current response.
*/
var value = $$.response.headers.get(key);

/*
    Set the current response's headers.

    Returns
      headers ({
        key: value
      }) - The new HTTP headers object for the current response.
*/
$$.response.headers.set(headers);

/*
    Set the current response's headers.

    Arguments
      key (string) - The key of the headers value to set.
      value (string) - The HTTP headers value to set at the given key.
*/
$$.response.headers.set(key, value);

/*
    Add the give value to the current key. If key isn't defined behaves like $$.response.headers.set.

    Arguments
      key (string) - The key of the headers value to add to.
      value (string) - The HTTP headers value to add at the given key.
*/
$$.response.headers.add(key, value);

/*
    Del the current response's headers at key.

    Arguments
      key (string) - The key to delete on the headers string.
*/
$$.response.headers.del(key);
```

##### Cookies Get / Set

```js
/*
    Get all HTTP Cookies on response.

    Returns
      cookies ({
        name: {
          value: string,
          path: string,
          domain: string,
          expires: date,
          secure: bool,
          httponly: bool,
          maxage: int
        }
      }) - A map of cookies on $$.response.
*/
var cookies = $$.response.cookies.get();

/*
    Get the HTTP Cookie at given name on the current response.

    Arguments
      name (string) - The name of the HTTP Cookie to get.

    Returns
      cookie ({
        value: string,
        path: string,
        domain: string,
        expires: date,
        secure: bool,
        httponly: bool,
        maxage: int
      }) | undefined - The HTTP Cookie for the given name. If the cookie doesn't exist then cookie will be undefined.
*/
var cookie = $$.response.cookies.get(name);

/*
    Set all HTTP Cookies on response.

    Arguments
      cookies ({
        name: {
          value: string,
          path: string,
          domain: string,
          expires: date,
          secure: bool,
          httponly: bool,
          maxage: int
        }
      }) - A map of new cookies to set on $$.response.
*/
$$.response.cookies.set(cookies);

/*
    Set HTTP Cookie on response.

    Arguments
      name (string) - The name of the cookie to set.
      value (string) - The value of the cookie to set.
*/
$$.response.cookies.set(name, value);

/*
    Set HTTP Cookie on response.

    Arguments
      name (string) - The name of the cookie to set.
      value (string) - The value of the cookie to set.
      options ({
        path: string,
        domain: string,
        expires: date,
        secure: bool,
        httponly: bool,
        maxage: int
      }) - Additional values to set on the cookie.
*/
$$.response.cookies.set(name, value, options);
```

##### Body Get / Set

```js
/*
    Get the current response body.

    Returns
      body (object) | undefined - The current response body, if there is no body on the response then undefined is returned.
*/
var body = $$.response.body.get();

/*
    Get the value on the current response body at the given path.

    Arguments
      path (string) - Path is the location of the value to return from the current response body.

    Returns
      value (object) | undefined - The value at the given path on the response body. If the value doesn't exist then undefined is returned.
*/
var value = $$.response.body.get(path);

/*
    Set the current response body.

    Arguments
      body (object) - The new response body to set.
*/
$$.response.body.set(body);

/*
    Set the value at the given path on the current response body.

    Arguments
      path (string) - Path is the location of the value to set on the current response. If path doesn't exist then try to create it.
      value (object) - The value to set at the given path.
*/
$$.response.body.set(path, value);
```

# Dollar Sign - $

```js
/*

*/
$.ctx.get => function()
$.ctx.get => function(path)

$.ctx.set => function(obj)
$.ctx.set => function(path, obj)
```

```js
/*

*/
$.stop => function()
```

# Steps

```js
/*

*/
stop => function()
```

```js
/*

*/
tests => object;
```

## HTTP

#### Step Request aka input

##### Get / Set

```js
/*
    Get the whole request object.

    Returns
      object ({
        method: string,
        url: string,
        headers: {
          key: value,
        },
        body: object
      }) - The current request coming into prism.
*/
var request = input.get();

/*
    Get a value on the request object at a given path.

    Arguments
      string - The path to fetch on the request object.

    Returns
     value (object) | undefined - The current request coming into prism. If path isn't found, then undefined is returned.
*/
var value = input.get(string);

/*
    Set the whole request object.

    Arguments
      object ({
        method: string,
        url: string,
        headers: {
          key: value,
        },
        body: object
      }) - Set the current request coming into Prism.
*/
input.set(object);

/*
    Set a value on the request object at a given path.

    Arguments
      string - The path to set on the request object. Will try to create appropriate
      object - The object to set at given path.
*/
input.set(string, object);
```

##### Method Get / Set

```js
/*
    Get the current request's method.

    Returns
      method (string) - The HTTP method for Double Dollar Sign Request.
*/
var method = input.method.get();

/*
    Set the current request's method.

    Arguments
      method (string) - The new HTTP method for Double Dollar Sign Request.
*/
input.method.set(method);
```

##### URL Get / Set

```js
/*
    Get the current request's url.

    Returns
      url (string) - The HTTP url for Double Dollar Sign Request.
*/
var url = input.url.get();

/*
    Set the current request's url.

    Arguments
      url (string) - The new url for Double Dollar Sign Request.
*/
input.url.set(url);
```

##### Path Get / Set

```js
/*
    Get the current request's path.

    Returns
      path (string) - The HTTP path for Double Dollar Sign Request.
*/
var path = input.path.get();

/*
    Set the current request's path.

    Arguments
      path (string) - The new path for Double Dollar Sign Request.
*/
input.path.set(path);
```

##### Scheme Get / Set

```js
/*
    Get the current request's scheme.

    Returns
      scheme (string) - The HTTP scheme for Double Dollar Sign Request.
*/
var scheme = input.scheme.get();

/*
    Set the current request's scheme.

    Arguments
      scheme (string) - The new scheme for Double Dollar Sign Request.
*/
input.scheme.set(scheme);
```

##### Host Get / Set

```js
/*
    Get the current request's host.

    Returns
      host (string) - The HTTP host for Double Dollar Sign Request.
*/
var host = input.host.get();

/*
    Set the current request's host.

    Arguments
      host (string) - The new host for Double Dollar Sign Request.
*/
input.host.set(host);
```

##### Query Get / Set / Add / Del

```js
/*
    Get the current request's query.

    Returns
      query ({
        key: value
      }) - The HTTP query object for Double Dollar Sign Request.
*/
var query = input.query.get();

/*
    Get the current request's query.

    Arguments
      key (string) - The key of the query value to get.

    Returns
      value (string) - The HTTP query value at the given key for Double Dollar Sign Request.
*/
var value = input.query.get(key);

/*
    Set the current request's query.

    Returns
      query ({
        key: value
      }) - The new HTTP query object for Double Dollar Sign Request.
*/
input.query.set(query);

/*
    Set the current request's query.

    Arguments
      key (string) - The key of the query value to set.
      value (string) - The HTTP query value to set at the given key.
*/
input.query.set(key, value);

/*
    Add the give value to the current key. If key isn't defined behaves like input.query.set.

    Arguments
      key (string) - The key of the query value to add to.
      value (string) - The HTTP query value to add at the given key.
*/
input.query.add(key, value);

/*
    Del the current request's query at key.

    Arguments
      key (string) - The key to delete on the query string.
*/
input.query.del(key);
```

##### Headers Get / Set / Add / Del

```js
/*
    Get the current request's headers.

    Returns
      headers ({
        key: value
      }) - The HTTP headers object for Double Dollar Sign Request.
*/
var headers = input.headers.get();

/*
    Get the current request's headers.

    Arguments
      key (string) - The key of the headers value to get.

    Returns
      value (string) - The HTTP headers value at the given key for Double Dollar Sign Request.
*/
var value = input.headers.get(key);

/*
    Set the current request's headers.

    Returns
      headers ({
        key: value
      }) - The new HTTP headers object for Double Dollar Sign Request.
*/
input.headers.set(headers);

/*
    Set the current request's headers.

    Arguments
      key (string) - The key of the headers value to set.
      value (string) - The HTTP headers value to set at the given key.
*/
input.headers.set(key, value);

/*
    Add the give value to the current key. If key isn't defined behaves like input.headers.set.

    Arguments
      key (string) - The key of the headers value to add to.
      value (string) - The HTTP headers value to add at the given key.
*/
input.headers.add(key, value);

/*
    Del the current request's headers at key.

    Arguments
      key (string) - The key to delete on the headers string.
*/
input.headers.del(key);
```

##### Content Types Content Negotiation

```js
/*
    Parses the Accept header and returns an ordered list of mime types that the client will accept.

    Returns
      accepts ([string]) - The types that the request accepts, in the order of the client's preference (most preferred first).
*/
var accepts = input.accepts.contentTypes.get();
```

##### Cookies Get / Set

```js
/*
    Get all HTTP Cookies on request.

    Returns
      cookies ({
        name: {
          value: string,
          path: string,
          domain: string,
          expires: date,
          secure: bool,
          httponly: bool,
          maxage: int
        }
      }) - A map of cookies on input.
*/
var cookies = input.cookies.get();

/*
    Get the HTTP Cookie at given name on the current request.

    Arguments
      name (string) - The name of the HTTP Cookie to get.

    Returns
      cookie ({
        value: string,
        path: string,
        domain: string,
        expires: date,
        secure: bool,
        httponly: bool,
        maxage: int
      }) | undefined - The HTTP Cookie for the given name. If the cookie doesn't exist then cookie will be undefined.
*/
var cookie = input.cookies.get(name);

/*
    Set all HTTP Cookies on request.

    Arguments
      cookies ({
        name: {
          value: string,
          path: string,
          domain: string,
          expires: date,
          secure: bool,
          httponly: bool,
          maxage: int
        }
      }) - A map of new cookies to set on input.
*/
input.cookies.set(cookies);

/*
    Set HTTP Cookie on request.

    Arguments
      name (string) - The name of the cookie to set.
      value (string) - The value of the cookie to set.
*/
input.cookies.set(name, value);

/*
    Set HTTP Cookie on request.

    Arguments
      name (string) - The name of the cookie to set.
      value (string) - The value of the cookie to set.
      options ({
        path: string,
        domain: string,
        expires: date,
        secure: bool,
        httponly: bool,
        maxage: int
      }) - Additional values to set on the cookie.
*/
input.cookies.set(name, value, options);
```

##### Body Get / Set

```js
/*
    Get the current request body.

    Returns
      body (object) | undefined - The current request body, if there is no body on the request then undefined is returned.
*/
var body = input.body.get();

/*
    Get the value on the current request body at the given path.

    Arguments
      path (string) - Path is the location of the value to return from the current request body.

    Returns
      value (object) | undefined - The value at the given path on the request body. If the value doesn't exist then undefined is returned.
*/
var value = input.body.get(path);

/*
    Set the current request body.

    Arguments
      body (object) - The new request body to set.
*/
input.body.set(body);

/*
    Set the value at the given path on the current request body.

    Arguments
      path (string) - Path is the location of the value to set on the current request. If path doesn't exist then try to create it.
      value (object) - The value to set at the given path.
*/
input.body.set(path, value);
```

#### Authentication

```js
/*

*/
// TODO: Should link them to the scenario specification auth object
// TODO: Verify that the auth api works like below.
input.auth.get => function()
input.auth.get => function(path)

input.auth.set => function(value)
input.auth.set => function(path, value)
```

#### Step Response

TODO: Description, should talk about how output is different from $$.response.

##### Get / Set

```js
/*
    Get the whole response object.

    Returns
      object ({
        status: int,
        time: int,
        headers: {
          key: value,
        },
        body: object
      }) - The current response object.
*/
var response = output.get();

/*
    Get a value on the response object at a given path.

    Arguments
      string - The path to fetch on the response object.

    Returns
     value (object) | undefined - The current value at the path on the response. If path isn't found, then undefined is returned.
*/
var value = output.get(string);

/*
    Set the whole response object.

    Arguments
      object ({
        status: int,
        headers: {
          key: value,
        },
        body: object
      }) - Set the current response object.
*/
output.set(object);

/*
    Set a value on the response object at a given path.

    Arguments
      string - The path to set on the response object. Will try to create appropriate objects at path if it doesn't exist.
      object - The object to set at given path.
*/
output.set(string, object);
```

##### Status Code Get / Set

```js
/*
    Get the current response's status code.

    Returns
      status (int) - The HTTP status code for the current response.
*/
var status = output.status.get();

/*
    Set the current response's status code.

    Arguments
      status (int) - The new HTTP status code for the current response.
*/
output.status.set(status);
```

##### Time Get

```js
/*
    Get round trip time.

    Returns
      roundTrip (int) - The time it took for the current reqeust to respond in milliseconds.
*/
var roundTrip = output.time.get();
```

##### Headers Get / Set / Add / Del

```js
/*
    Get the current response's headers.

    Returns
      headers ({
        key: value
      }) - The HTTP headers object for the current response.
*/
var headers = output.headers.get();

/*
    Get the current response's headers.

    Arguments
      key (string) - The key of the headers value to get.

    Returns
      value (string) - The HTTP headers value at the given key for the current response.
*/
var value = output.headers.get(key);

/*
    Set the current response's headers.

    Returns
      headers ({
        key: value
      }) - The new HTTP headers object for the current response.
*/
output.headers.set(headers);

/*
    Set the current response's headers.

    Arguments
      key (string) - The key of the headers value to set.
      value (string) - The HTTP headers value to set at the given key.
*/
output.headers.set(key, value);

/*
    Add the give value to the current key. If key isn't defined behaves like output.headers.set.

    Arguments
      key (string) - The key of the headers value to add to.
      value (string) - The HTTP headers value to add at the given key.
*/
output.headers.add(key, value);

/*
    Del the current response's headers at key.

    Arguments
      key (string) - The key to delete on the headers string.
*/
output.headers.del(key);
```

##### Cookies Get / Set

```js
/*
    Get all HTTP Cookies on response.

    Returns
      cookies ({
        name: {
          value: string,
          path: string,
          domain: string,
          expires: date,
          secure: bool,
          httponly: bool,
          maxage: int
        }
      }) - A map of cookies on output.
*/
var cookies = output.cookies.get();

/*
    Get the HTTP Cookie at given name on the current response.

    Arguments
      name (string) - The name of the HTTP Cookie to get.

    Returns
      cookie ({
        value: string,
        path: string,
        domain: string,
        expires: date,
        secure: bool,
        httponly: bool,
        maxage: int
      }) | undefined - The HTTP Cookie for the given name. If the cookie doesn't exist then cookie will be undefined.
*/
var cookie = output.cookies.get(name);

/*
    Set all HTTP Cookies on response.

    Arguments
      cookies ({
        name: {
          value: string,
          path: string,
          domain: string,
          expires: date,
          secure: bool,
          httponly: bool,
          maxage: int
        }
      }) - A map of new cookies to set on output.
*/
output.cookies.set(cookies);

/*
    Set HTTP Cookie on response.

    Arguments
      name (string) - The name of the cookie to set.
      value (string) - The value of the cookie to set.
*/
output.cookies.set(name, value);

/*
    Set HTTP Cookie on response.

    Arguments
      name (string) - The name of the cookie to set.
      value (string) - The value of the cookie to set.
      options ({
        path: string,
        domain: string,
        expires: date,
        secure: bool,
        httponly: bool,
        maxage: int
      }) - Additional values to set on the cookie.
*/
output.cookies.set(name, value, options);
```

##### Body Get / Set

```js
/*
    Get the current response body.

    Returns
      body (object) | undefined - The current response body, if there is no body on the response then undefined is returned.
*/
var body = output.body.get();

/*
    Get the value on the current response body at the given path.

    Arguments
      path (string) - Path is the location of the value to return from the current response body.

    Returns
      value (object) | undefined - The value at the given path on the response body. If the value doesn't exist then undefined is returned.
*/
var value = output.body.get(path);

/*
    Set the current response body.

    Arguments
      body (object) - The new response body to set.
*/
output.body.set(body);

/*
    Set the value at the given path on the current response body.

    Arguments
      path (string) - Path is the location of the value to set on the current response. If path doesn't exist then try to create it.
      value (object) - The value to set at the given path.
*/
output.body.set(path, value);
```
