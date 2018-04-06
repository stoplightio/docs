# Introduction

Prism is a proxy and API server toolkit that helps you test, mock, validate, and orchestrate your online applications. We rebuilt Prism from the ground up to be performant, powerful, and programmable while still being practical. Prism enables teams to work in parallel and iterate faster with less errors. The Stoplight Platform integrates tightly with Prism to generate test coverage of your API automatically, build tests visually, and create mock and contract servers instantly.

Prism has first class support for the OpenAPI Specification (aka OAS) and Stoplight Scenarios. OAS is machine readable documentation of your API that Prism can read and understand. Scenarios tell Prism how to orchestrate your API. When you use them together you can easily assert, transform, and validate your API against your OAS. Prism also allows your front-end team to work in tandem with your back-end team. While the back-end team implements your API, your front-end teams can implement against a mock server that can return static examples, dynamic data, or replay actual traffic from your API.

![Prism Overivew](https://github.com/stoplightio/docs/blob/develop/assets/images/prism-introduction-help.png?raw=true)

## Features

* Act as a mock server, routing incoming requests to example responses, or dynamically generating examples on the fly
* Act as a transformation layer, manipulating incoming requests and outgoing responses
* Act as a validation layer, validating incoming requests, and outgoing responses
* Contract test your APIs
* Extend existing APIs with new endpoints or capabilities
* Act as a system-wide proxy, blocking traffic to particular websites or endpoints

## Conduct vs Serve

Conduct and Serve are important concepts to understand when using Prism.

* Conduct is an isolated scenario run. You tell Prism what scenarios you want to run, give it an environment to run against, and Prism will generate a report of the run

* Serving, on the other hand, is a long running instance of Prism that applies scenarios to HTTP traffic

### Conduct Use Cases

1.  Debugging your API implementation or specification
2.  Integrating with your CI/CD Environment: Catch bugs before they get to your actual API Consumers
3.  Webhooks: Generate your OAS from code, automatically upload it to Stoplight

![Prism Conduct](https://github.com/stoplightio/docs/blob/develop/assets/gifs/prism-introduction-conduct.gif?raw=true)

### Serve Use Cases

1.  Mocking back one or more specifications: Useful to help teams work in parallel and simplify testing dependencies.
2.  Validating live traffic between your client/backend.
3.  Your API, your workflow, your Prism. Prism is very flexible. You can easily create an instance that will record your API traffic, save it to S3, and then create another instance that will replay that API traffic.

![](../../assets/gifs/prism-introduction-mock.gif)

### Stoplight Prism Helpers

The [Prism Helpers](https://next.stoplight.io/stoplight/prism) project is a collection of scenarios, specifications, and Prism instances that illustrate how to use Prism effectively. Please go [here](https://community.stoplight.io) and let us know what you would like to see.

---

**Related Articles**

* [Javascript Runtime Refrence](/runtime.md)
* [Passing Data Between Steps](/testing/getting-started/passing-data-between-steps)
* [Running Tests In Stoplight](/testing/running-tests/in-stoplight)
* [Running Tests in the Terminal](/testing/running-tests/in-the-terminal)
* [Running Tests Triggered by URL](/testing/running-tests/triggering-by-url)
* [Using Variables Overview](/testing/using-variables/overview)
* [$$.env (Environment)](/testing/using-variables/environment)
* [$.ctx(Context)](/testing/using-variables/context)
* [Sending HTTP Requests](/testing/sending-http-requests/overview)
* [Referencing other Scenarios](/testing/referencing-other-scenarios/overview)
* [Contract Testing](/testing/leveraging-openapi/contract-testing)
* [Integrating in Continuous Integration](/testing/continuous-integration/overview)
