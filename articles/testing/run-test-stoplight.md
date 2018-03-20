# Running Scenarios

Scenarios allow you to quickly and efficiently test APIs. Scenarios can be
run in a variety of different ways, including from the [command-line with
Prism](/testing/running-tests/in-the-terminal) or by [URL](/testing/running-tests/triggering-by-url). However, the easiest
way is through the Stoplight editor.


> If you haven't created your first scenario yet, please [do so before
> continuing](testing/introduction)

Scenarios in Stoplight are composed of three different levels:

* **Steps**: low-level building blocks that compose a scenario.
  Steps allow you to easily chain individual actions (e.g., performing a
  web request) together, enabling for more complex testing workflows.

* **Scenarios**: a series of **steps** that perform a high-level
  action (e.g., registering a new user).

* **Collections**: a series of **scenarios** that encapsulate an
  entire test suite. Collections are the highest-level building blocks for creating
  a library of API interactions and tests.

Each level above can be run individually or all together.

## Running a Step

Once you have created a scenario **step**, use the **Run Step** button to
execute that step. The **Run Step** button is available towards the top of the
editor, as shown below.

![](../../assets/images/run-test-stoplight.png)

## Running a Scenario

Once you have added enough steps to a **scenario**, use the **Run Scenario**
button to execute that scenario. The **Run Scenario** button is available
towards the top of the editor while viewing the scenario configuration/overview,
as show below.

![](../../assets/images/run-test-stoplight2.png)


> Scenarios can also be run directly from every step using the **Run Scenario**
> button

## Running a Collection

Once you have added created enough scenarios to compose a **collection**, use
the **Run Collection** button to run the entire collection (including all
scenarios and steps). The **Run Collection** button is available towards the top
of the editor while viewing the collection home screen, as shown below.

![](../../assets/images/run-test-stoplight3.png)


> Collections can also be run from the scenario and step screens using the **Run
> Collection** button

---

**Related Articles**
- [Testing Introduction](/testing/introduction)
- [Running Tests in the Terminal](/testing/running-tests/in-the-terminal)
- [Running Tests Triggered by URL](/testing/running-tests/triggering-by-url)

