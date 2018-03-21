# Shared Parameters and Responses

While designing API's in Stoplight, it is common to have multiple endpoints
share a set of query parameters and API responses. To help reduce extra
work (and the chance of introducing errors), it is important to: 

* Identify endpoints with common parameters 
* Use _shared components_ to reference the same property multiple times instead
  of rewriting the properties for each individual endpoint.

Shared components in Stoplight come in two forms:

* __Parameters__ - These are shared parameters that can be applied to requests
  across multiple endpoints.

* __Responses__ - These are shared response objects that can be applied to
  multiple endpoints.

## Parameters

Shared parameters provide a way to use request properties across multiple API
endpoints without having to duplicate effort.

![How to create a shared parameter](https://github.com/stoplightio/docs/blob/develop/assets/gifs/shared-params-responses-param.gif?raw=true)

Shared parameters are supported in the following request property locations:

  * __path__ - The request URL path
  * __query__ - The request URL query string
  * __header__ - The request HTTP Header field object
  * __body__ - The request HTTP message body
  * __form-data__ - The request HTTP message body in the `multipart/form-data` format 

> For more information the above properties, see the [OpenAPI v2 Specification](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md#parameter-object)

Similar to generic request parameters, restrictions on the parameter values can
also be applied based on type, expected default value, minimum/maximum length,
and regular expression (regex).

![Create a reference to a shared parameter](https://github.com/stoplightio/docs/blob/develop/assets/images/shared-params-responses.png?raw=true)

To use a shared parameter, navigate to an API endpoint's _Request_ section and
create a reference to the shared parameter using the "chain" button as shown in
the image above. Once the parameter has been referenced, any updates to the
shared parameter will automatically be propagated to every endpoint using that
parameter.

![Reference as a query parameter](https://github.com/stoplightio/docs/blob/develop/assets/gifs/shared-params-responses-param2.gif?raw=true)

Like other references in Stoplight, shared parameters can also be shared across
files, projects, and other external sources.

### Shared Parameters Example

Let's say you are creating an API to serve thousands of cooking recipes. When dealing with large volumes of
data, you typically want to avoid sending _all_ data in a request. To help avoid
sending more data than is necessary, most applications implement a "paging"
feature that allows clients to retrieve a small portion of results (i.e. a single
page).

There are multiple ways to approach a paging feature. For this example, we
want to add two query string parameters to every request:

* `limit` - The number of results to return when viewing a page. For example,
  setting `limit` to `20` means that, at most, 20 results will be returned in the
  request.
* `offset` - The number of results to skip before returning results. For
  example, setting an `offset` of `20` means that the API will discard the first
  20 results.

By using the two parameters above, a client can efficiently "page" through
results, only returning items that are within the requested bounds. To demonstrate, let's use the parameters to display the first page of our recipe
results:

```
GET /recipes?limit=20&offset=0
```

Since the `offset` is set to `0`, the API will not discard any results. Paired
with a `limit` of `20`, we will only see the first 20 results (1 through 20). 

To view the second page of recipes, we would use:

```
GET /recipes?limit=20&offset=20
```

By setting an `offset` of `20`, the API will discard the first 20 results. Paired
again with a `limit` of `20`, we will see the second page of results (21 through
40).

### How
Now that we know how we want the components to behave, let's create them in
Stoplight. To get started, create a new shared parameter for an OpenAPI file
under the "Shared" section of the menu.

![Instructions below](https://github.com/stoplightio/docs/blob/develop/assets/images/shared-params-responses2.png?raw=true)

As shown in the image above, set the properties for each parameter based on our
requirements:

1. Be sure to set the display names for both components properly. In our
   example, we only have two parameters, however, if there are multiple shared
   parameters with similar names, you may want to set a more descriptive name
   (i.e. 'recipe-limit' instead of 'limit').
2. Since both components are query string parameters, set the property location
   for each as 'query'.
3. Set the name of the parameter, which is how it will be set in HTTP requests.
4. Optional type restrictions can be applied to the values. In our case, since
   both parameters are integer values, we can use the 'integer' format
   restriction.
5. Setting a default value can be useful if you don't need the client to specify
   each parameter for every request. For our example, it makes sense to set
   defaults that will return the first page (limit of 20, offset of 0).

![Linking a shared parameter](https://github.com/stoplightio/docs/blob/develop/assets/images/shared-params-responses3.png?raw=true)

Once the shared parameters are created, reference them in any API endpoint under the
__Query Parameters__ block of the request section in the editor.

## Shared Responses

Shared responses provide a practical way to re-use response objects across multiple API
endpoints without having to duplicate effort. Similar to the shared components
discussed above, shared responses allow you to reference a single response
multiple times without having to recreate each response manually. The added
benefit of this approach is that updates to the shared response object are
automatically propagated to any endpoint using that object, no extra changes
required.

![How to create a shared response](https://github.com/stoplightio/docs/blob/develop/assets/gifs/shared-params-responses-response.gif)

Shared responses allow you to configure the following properties:

* Headers - Customize the HTTP Headers returned in the response
* Response body - Customize the HTTP message body contents using the Stoplight
  modeling tool (or reference a pre-existing model)


> For more information on the above properties, see the OpenAPI v2 Specification
  [here](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md#responseObject)

![](../../assets/gifs/shared-params-responses-response2.gif?raw=true)

To use a shared response, navigate to an API endpoint's __Response__ section and
create a reference to the shared response by choosing the _Type_ of the response
as "Reference". Once the Response type is set to "Reference", you can then
choose the shared response to use for that endpoint. Shared responses can also
be shared across files, projects, and other external sources.

### Shared Responses Example

Let's say you have a set of
API endpoints that should return the same error response when a failure occurs.
Every time an error is returned from the API, you want to make sure the
following properties are returned:

* `error_message` - A descriptive error message about the failure in string format.
* `error_code` - A code representing the category of the failure in integer format.
* `tracking_id` - A tracking ID that can be used by the caller to follow-up with
  an administrator for more information (ie, debug an issue with customer
  support).

Now that we know what should be returned, let's create a shared response in
Stoplight. To get started, create a new shared response for an OpenAPI file
under the "Shared" section of the menu.

![](https://github.com/stoplightio/docs/blob/develop/assets/images/shared-params-responses4.png?raw=true)

As shown in the image above, set the properties for each portion of the response
based on our requirements:

1. Set the name of the shared response. In our example, we only have one error
   type, however, if there are multiple error responses with similar names, you
   may want to set a more descriptive name (ie, 'api-tracking-error' instead of
   'error').
2. A short description of the error response, such as why it is needed and how
   it is used.
3. The contents of the shared response object based on the three required
   properties above.

![](https://github.com/stoplightio/docs/blob/develop/assets/images/shared-params-responses5.png?raw=true)

Once the shared response is created, it can be referenced in any API endpoint by
using a _Reference_ type under a response. A shared response can also be used
multiple times under the same endpoint.

***

**Related**

* [OpenAPI v2 Parameter Objects Reference](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md#parameter-object)
* [OpenAPI v2 Response Objects Reference](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md#responseObject)
