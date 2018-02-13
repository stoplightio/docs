# Contract Testing

Scenarios makes it easy to incorporate your OAS / Swagger API specification into your testing process. A few benefits to doing this include:

- **DRY**: Don't re-create test assertions that check for what is already described in your API contract.
- **Governance**: Quickly figure out if the API that was created actually conforms to the API design that was initially agreed upon.
- **Sync Manager**: Your API spec is the single point of truth that describes your API. From it, you might generate documentation, sdks, mock servers, etc. Incorporating your spec into your tests makes sure that your API spec accurately represents your API over time.

<!-- theme: info -->
> If you don't have an API specification yet, you can create one using the Stoplight modeling tool!

## Connecting The Spec

The first thing you need to do to get started with contract testing is connect your API spec to the Scenarios Collection.

1. Create a new (or open an existing) **Scenario file** in the Stoplight editor
2. Select **Swagger/OAS Coverage** in the Scenarios menu to the left
3. Open **Contract Test Settings**
4. Click **+ Add Spec**
5. Select a file from either **This Project** or an **External URL**
6. You are all set! You can now test against an API spec. 

## Using the Coverage Report

The coverage report gives you a quick overview of which parts of the connected specs are covered by test assertions in the current Scenario Collection.

You can use the coverage report to quickly stub out a new scenario. Just click the status codes in the table matrix for the steps you want to add to your scenario (in order). Once you've added all the steps, click the "Create Scenario" button in the top right. This will create a scenario with as much setup as possible, using the connected spec for data. It will set your request body, set variables in a sensible way, automatically setup contract tests, and more.

You will likely need to tweak the resulting scenario a little bit, but this process will usually get you most of the way to a complete scenario, with contract test assertions in place!

## Automatic Contract Test Assertion

After linking your spec to the Scenario Collection, contract test assertions will be automatically added for step assertions.

Stoplight will look through your API specification for a operation that matches the step's HTTP method + URL, and use the response status code returned from the API to look up the JSON schema. In the example below, we are testing the 200 response schema in our API spec for the GET /todos/{todoId} endpoint.

When this step is run, the HTTP response structure will be validated against the matched JSON schema from our API spec, and any errors will be added to the test results.
