# Contract Testing

Scenarios makes it easier than ever to integrate your OpenAPI specification into
your testing process. One of the easiest ways to do this is through a testing
method called **contract testing**. Contract testing is a simple verification
process where Stoplight verifies that the API responses match the "contract"
within a connected OpenAPI specification.

Benefits of contract testing include:

* **Don't Repeat Yourself**: Don't re-create test assertions that check for what
  is already described in your API specification. Let your scenario do the heavy
  lifting, validating that an API implementation matches the OpenAPI
  specification.

* **Governance**: Quickly figure out if an API implementation conforms to the
  OpenAPI specification that was initially agreed upon. Run a contract test
  scenario on a schedule to ensure the API never violates the specification.

* **Single Source of Truth**: Your API specification is the single source of
  truth that describes your API. From it, you can generate documentation, SDKs,
  mock servers, and more. Incorporating the specification into your testing
  pipeline ensures that the spec accurately represents your API implementation
  over time.

> If you don't have an API specification yet, you can create one using the
> [Stoplight modeling tool](/modeling/introduction)!

## Connecting a Spec

![Connecting a Spec](https://github.com/stoplightio/docs/blob/develop/assets/gifs/contract-test-add-spec.gif?raw=true)

To get started with contract testing, the first thing you will need to do is
generate a scenario from an OpenAPI specification. To get started:

1.  Create a new (or open an existing) **scenario** in the Stoplight editor
2.  Select **Swagger/OAS Coverage** in the Scenarios menu to the left
3.  Open the **Contract Test Settings** menu
4.  Click **Add Spec**, and select an OpenAPI specification to connect

You are all set! Once the specification has been connected, you can
automatically generate a contract testing scenario for your spec using the
Coverge Report, as described below.

## Using the Coverage Report

The coverage report gives you a quick overview of which parts of the connected
specs are covered by test assertions in the current Scenario Collection.

You can use the coverage report to quickly stub out a new scenario. To start:

1.  Click the **status codes** in the table matrix for the steps you want to add to
    your scenario.


> Note that the order in which the endpoints are clicked
> determines the order in which they will appear in the scenario. For example,
> if an API object needs to be created before it can be removed, then you will
> want to choose the 'create object' endpoint before the 'delete object'
> endpoint.

2.  Once all of the desired endpoints have been selected, click the **Create
    Scenario** button in the top right to generate the scenario.

3.  You will automatically be navigated to the new scenario, complete with
    contract test assertions for each selected endpoint.

> You will likely need to modify the resulting scenario to fit your use case

## Automatic Contract Test Assertion

![Running a Collection](https://github.com/stoplightio/docs/blob/develop/assets/gifs/testing-run-results.gif?raw=true)

After linking your spec to the Scenario Collection, contract test assertions
will be automatically added as steps within your scenario.

When the scenario is generated, Stoplight will look through the API
specification for an operation that matches the step's HTTP method and URL. The
response code returned from the API is then used to look up the corresponding
JSON schema.

When a contract assertion step is run, the HTTP response structure will be
validated against the matched JSON schema from the connected API specification.
Any validation errors will automatically be added to the test results.

---
**Related Articles**
- [Testing Introduction](/testing/introduction)
- [Running Tests In Stoplight](/testing/running-tests/in-stoplight)
- [Running Tests in the Terminal](/testing/running-tests/in-the-terminal)
- [Running Tests Triggered by URL](/testing/running-tests/triggering-by-url)
- [Using Variables Overview](/testing/using-variables/overview)
- [$$.env (Environment)](/testing/using-variables/environment)
- [$.ctx(Context)](/testing/using-variables/context)
- [Sending HTTP Requests](/testing/sending-http-requests/overview)
- [Referencing other Scenarios](/testing/referencing-other-scenarios/overview)
