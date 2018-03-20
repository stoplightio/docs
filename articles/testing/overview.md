# Testing with Scenarios

Following the rise of APIs, it has become increasingly important to develop highly flexible, performant, and powerful testing roadmaps to catch bugs faster and rapidly iterate without breaking existing features. A thorough test suite is essential for: 
- Assessing the health of an API
- Providing valuable documentation 
- Driving design and implementation 
- Managing technical debt 

## Assessing the Health of an API

APIs require maintenance like any other software. To ensure that your API is functioning properly, a suite of tests should be run periodically to check for weaknesses and errors.  

>Create and [run tests within Stoplight](/testing/running-tests/in-stoplight), [the terminal](/testing/running-tests/in-the-terminal), or [trigger it by URL](/testing/running-tests/triggering-by-url). If you prefer to [use CI](/testing/continuous-integration/overview), Stoplight also provides integrations to [Jenkins](/testing/continuous-integration/jenkins), [CircleCI](/testing/continuous-integration/circle-ci), and [Travis](/testing/continuous-integration/travis).  

## Providing Valuable Documentation & Driving Design

API tests provide insight into how your API behaves under certain scenarios and can drive design if created early enough in the design process. Test/Behavior-driven development (TDD/BDD) encourages you to think about design requirements before writing any code. 

>Stoplight further promotes this design first principle by providing [Contract Testing](/testing/leveraging-openapi/contract-testing); an integration between your tests and your OpenAPI Specification. This allows for immediate validation and verification that your API responses match the “Contract” specified in your OpenAPI spec.

## Managing Technical Debt 

Microservices and serverless architecture have made it easier than ever to iterate quickly. The downside of rapid development is an increase in bugs and technical debt, making projects harder to manage without a proper testing solution. It is critical to have a comprehensive test suite to allow teams to test the API during development. 

>Stoplight makes it easy to create a full suite of tests by providing [Environment](/testing/using-variables/environment) and [Context variables](/testing/using-variables/context), and the ability to [reference other scenarios](/testing/referencing-other-scenarios/overview) to accelerate test generation and reduce duplication. 

---
**Related Articles**
- [Passing Data Between Steps](/testing/getting-started/passing-data-between-steps)
- [Running Tests In Stoplight](/testing/running-tests/in-stoplight)
- [Running Tests in the Terminal](/testing/running-tests/in-the-terminal)
- [Running Tests Triggered by URL](/testing/running-tests/triggering-by-url)
- [Using Variables Overview](/testing/using-variables/overview)
- [$$.env (Environment)](/testing/using-variables/environment)
- [$.ctx(Context)](/testing/using-variables/context)
- [Sending HTTP Requests](/testing/sending-http-requests/overview)
- [Referencing other Scenarios](/testing/referencing-other-scenarios/overview)
- [Contract Testing](testing/leveraging-openapi/contract-testing)
- [Integrating in Continuous Integration](/testing/continuous-integration/overview)
- [Integrating with Jenkins](/testing/continuous-integration/jenkins)
- [Integrating with Travis](/testing/continuous-integration/travis)
- [Integrating with CircleCI](/testing/continuous-integration/circle-ci)
