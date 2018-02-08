# Continuous Integration

Continuous Integration (CI) is the practice of continuously merging developer
work into a shared repository. By merging work frequently, developers can easily
detect conflicts and stay up-to-date with other team members' changes. Since CI
allows teams to maintain a high development velocity, testing becomes an even
more crucial component to the development process. By constantly testing all
changes, developers can verify that they are not breaking existing functionality
or introducing new bugs.

By integrating Prism into your CI process, your development team can be certain
that any changes made to a project do not violate an OpenAPI specification. This
allows multiple teams with agreed-upon specifications to work independently of
one another, while ensuring that any changes meet the specification throughout
the lifetime of the project.

There are a few different approaches available when integrating Prism into a CI
testing pipeline: 
testing with Stoplight [Scenarios](./scenarios-introduction.md), 
testing with a mock server, and
contract testing.

## Testing with Scenarios

Stoplight [Scenarios](./scenarios-introduction.md) allows users to define
multiple steps for testing an OpenAPI specification. Scenarios provide a similar
function to API's as [functional test
cases](https://en.wikipedia.org/wiki/Functional_testing) do in software
development. Scenarios run (or "conducted") by Prism can be easily integrated
into a CI pipeline for validating a server's implementation of a specification.

To run a scenario with Prism, use the `conduct` command:

```bash
prism conduct --spec open-api-spec.json --path my-scenario.json -e "myapikey=abc123"
```

For more information on Scenarios, please see [here](./scenarios-introduction.md).

## Testing with a Mock Server

Prism's mock server allows Prism to behave like a
fully-implemented server for a provided OpenAPI specification. This form of
testing is useful for:

* **Speeding Up Development Time** 
    * Tests can be run locally with nothing more
  than an API specification. This allows a development team on the client or
  server side to work independently of one another.
* **Validation Testing** 
    * Ensures that a client implementation meets all of the requirements set by an
  OpenAPI specification.

To start a mock server with Prism, use the `mock` command:

```bash
prism mock --spec open-api-spec.json
```

For more information on mock testing with Prism, see [here](FIXME).

## Contract Testing

Contract testing is when Prism acts as a proxy between the client and a target
upstream server. When Prism receives a request, it forwards it to the upstream
server and validates that the server response conforms to the provided OpenAPI
specification. This form of testing is useful for:

* Verifying a _server_ implementation to ensure all _responses_ meet the
  appropriate requirements set by an OpenAPI specification.
* Verifying a _client_ implementation to ensure all _requests_ meet the
  appropriate requirements set by an OpenAPI specification.
* Augmenting existing test suites with very little extra work and almost no
  workflow changes required.

To start a contract/validation server with Prism, use the `validate` command:

```bash
prism validate --spec open-api-spec.json --upstream http://localhost:8080
```

For more information on contract testing with Prism, see [here](FIXME).

***

**Related**

* [Testing Overview](./overview.md)
* [Scenarios Introduction](./scenarios-introduction.md)
* [Continuous Integration with Circle CI](./continous-integration-circle.md)
* [Continuous Integration with Travis CI](./continous-integration-travis.md)
* [Continuous Integration with Jenkins](./continous-integration-jenkins.md)
