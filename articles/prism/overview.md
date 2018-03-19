# Introduction

Prism is a runtime orchestration engine built to help technical teams make modern APIs. We rebuilt Prism from the ground up to be performant, powerful, and programmable while still being practical. Prism enables teams to work in parallel and iterate faster with less errors. The Stoplight Platform integrates tightly with Prism to generate test coverage of your API automatically, build tests visually, and create mock and contract servers instantly.

Prism has first class support for the Open API Specfiction (aka OAS) and Stoplight Scenarios. OAS is machine readable documenation of your API that Prism can read and understand. Scenarios tell Prism how to orchestrate your API. When you use them together you can easily assert, transform, and validate your API against your OAS. Also, while the backend team implements your API, your front-end teams can implement against a mock server that can return static examples, dynamic data, or replay actual traffic from your API.

### Features

* Act as a mock server, routing incoming requests to example repsonses, or dynamically generating examples on the fly
* Act as a transformation layer, manipulating incoming requests and outgoing responses
* Act as a validation layer, validating incoming requests and outgoing responses
* Contract test your APIs, given an OAS(Swagger 2) file
* Log all or a subset of traffic to configurable locations
* Extend existing APIs with new endpoints or capabilites
* Act as a system-wide proxy, blocking traffic to particular websites or endpoints

## Conduct vs Serve

Conduct and Serve are important concepts to understand when using Prism. Conduct is an isolated scenario run. You tell Prism what scenarios you want to run, give it an environment to run against, and Prism will generate a report of the run. Serving, on the other hand, is a long running instance of Prism that applies scenarios to HTTP traffic.

[Diagram?]

### Conduct Use Cases

1.  Debugging your API implementation or specification
2.  Integrating with your CI/CD Environment. Catch bugs before they get to your actual API Consumers
3.  Webhooks. Generate your OAS from code, automatically upload it to Stoplight

#### Testing

TODO: Figure out if we can report the number of assertions from a contract test? For example, contract testing counts as only one assertion, but in reality if you have big response, each property is tested, and the value is asserted against.

Monoliths, microservices and serverless. Java, Javascript, Go, Python, and Erlang.

Stop writting unit tests in code and replace them with scenarios.

Sceanrios are powerful, fast and flexible way to test your API.

Run thousands of assertions in seconds, without writting any code. You already defined

Overview + links to all the testing related articles.

#### Orchestration? Some word.

Very short on this one. IFTT type use cases for conduct or triggered conduct. Callbacks

### Serve Use Cases?

Mostly just high level overview and links to other articles.

## Continuous Integration

… mostly just links to the relevant running prism in x situation articles and the CI articles.

---

**Further Reading**

One
Two

What
Scenarios
OAS
Instances
Mapping / Pointer System
Hosted vs. Binary

# Use Cases

Testing

Language independent

Easy assertions / transforms and powerful scripting

Automatic contract testing

Environments / Context

Javascript

Coverage Reports

Performant

Mocking / Validation / Rec-Repl Servers

What / Why

CI/CD Pipeline - Run Scenarios / Spin up instances

Your heart, Your desires

Orchestration engine first

Which brings flexibiity
