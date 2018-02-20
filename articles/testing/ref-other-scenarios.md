# Scenario References

References are a special type of step that allow you to include other scenarios in your scenario. This is a very powerful concept that can dramatically reduce the duplication in your scenarios.

To use them, simply add a step and change it's type from "HTTP/Script" to "REF". This will expose a dropdown that lists all of the scenarios in your collection. Select a value in this dropdown to create the ref to that scenario.

In the screenshot below, [Todo: Utility CRUD](https://next.stoplight.io/stoplight/hub/blob/master/tests.scenarios.yml?edit=%23%2Fscenarios%2Ftodo-utility) and [User: Utility CRUD](https://next.stoplight.io/stoplight/hub/blob/master/tests.scenarios.yml?edit=%23%2Fscenarios%2Fuser-utility) scenario have one step that refrences [Entity CRUD](https://next.stoplight.io/stoplight/hub/blob/master/tests.scenarios.yml?edit=%23%2Futilities%2Fcrud) from Utilities. Entity CRUD does all the heavey lifting: it creates, gets, updates, deletes and gets(To verify entity was deleted) an entity.

$.ctx values saved in ref steps **ARE** available in subsequent steps. The ref step in the screenshot below saves a $.ctx.accessToken property (not displayed), that the "Create Org" step then uses.

![](https://s3.amazonaws.com/cdn.stoplight.io/help-portal/scenarios/create+org+%2B+user+with+ref.png)
_need to update image_

### Viewing Reference Output

When a reference is run as part of a scenario, its output will expanded so that you can view the results of each step. In the screenshot below, we are looking at the results of the `Todo: Utitliy CRUD` scenario pictured above.

Tests and assertions made in a referenced scenario **will** contribute to the overall pass/fail count of the calling scenario.

![](https://s3.amazonaws.com/cdn.stoplight.io/help-portal/scenarios/view+ref+output.png)
_need to update image_

---

**Related**

* [Variables Overview](variables-overview.md)
* [Context Variables](variables-context.md)
* [Variables Environment](variables-environment.md)
