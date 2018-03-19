# API Models

Models are used to describe common structures in your API design. Use models to
describe common structures in your API design. Models help reduce duplication in
your API definitions, and increase future maintainability.

While designing your APIs, you will often find yourself repeating structures in
your endpoint request and response bodies. Models allow you to describe these
common structures, and then reference the object from endpoint definitions and
other models (with references).

## Effective API Model Design

An API model can be viewed as a blueprint that identifies the requirements for
an API development project. A well crafted API model indicates you understand
the problem you are trying to solve.

The following steps can help you get started with creating an excellent API
model.

### Identify Needs

During interactive sessions with stakeholders, outline all the requirements you
want your API to meet. Some important questions to ask:

* What goal(s) do we want to achieve with the API?
* Who are the principal users that will consume or interact with the API?
* What activities will the users execute?
* How can we group the activities into steps?
* What are the API methods that are required for these steps? (Place the methods into common resource groups.)
* What resources will the API expose?
* What permissions will we need?

This process may need to be repeated until the API development team is sure that
all requirements are covered.

### Build a Common Vocabulary

Vocabulary is used in your API artifacts such as your data fields, resource
names, identifiers, and documentation. Creating a standard vocabulary helps you:

* Communicate well with different audiences.
* Establish a standard or style guide that can be adopted by members of the API development team.
* Easily update your documentation.

### Identify Resource Relationships

If your resources contain references to other resources or contain child
resources, it is important to understand and define the types of relationships
between resources because this will help you to show the link between the
resources to the API user making the API more readable. Relationships can be:

* **Dependent**: the resource cannot exist without a parent resource.
* **Independent**: the resource can stand on its own and can reference another
  resource but does not need another resource to exist or function.
* **Associative**: the resources are independent but the relationship includes
  or needs further properties to describe it.

### Create a Test Plan

Ensuring that your API meets the agreed-upon specification requires testing.
Design test plans early.

Feasible tests you can execute include:

* **Functional Testing**: Test the API calls to ensure that it delivers or
  behaves as expected. For example, you can test to see that the API delivers
  the expected data based on your model.

* **Mocking** (service simulation): Mocking allows you to execute tests on an
  API deployment without calling it through a defined API key. Effective API
  tools will allow you to test your API before implementation.

* **Load Testing**: How will your API perform when deployed on a production
  server? A load test is one way to simulate the effect of traffic on your
  servers and observe the performance of your API when it is available to users.
  Doing a load test will help you understand your API threshold and if the users
  exceed the threshold.

---

**Related**

* [Modeling Introduction](/modeling/introduction)
* [Object Inheritance](/modeling/json-best-practices/object-inheritance)
* [Testing Overview](/testing/introduction)
* [Mock Testing with Prism](/mocking/introduction)
