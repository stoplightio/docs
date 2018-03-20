# Introduction

As APIs continue to spread throughout orginzations it is more important than ever to develop a highly flexible, performant and powerful testing roadmap. We all know why testing is important you can catch bugs faster, iterate without breaking existing features faster, and ultimately deliver a higher quality product to the end user. But lets be honest for a second. Even though we think testing is important we were too busy to actually write them. Also, maintaining a test suite is tedious, right? Lastly, we all write perfect code, no need to test it, plus 10k people thought that Stackoverflow answer was useful. Very compelling arguments if APIs weren't everywhere, otherwise those arguements are the reason why people aren't using your API.

API testing isn't about you actually and you know this deep down becuase there is nothing more frustrating than using an API that doesn't work as advertised. Your customers will appreciate a well tested service, but customers aren't the only people who will be using your API anymore. Team members are now users and they might be distrbuted in a different time zone, having an awesome test suite means that they can quickly know if a service is working as intended. There is nothing more frustrating than looking for some obscure bug in code you didn't write and in a language you don't know.

API testing also isn't just about catching bugs and iterating faster. A through test suite is actually really great documentation. Not only are test a great way to understand how an API works under certain Scenarios ;), they can also be a great way to drive your actual implementation if you create them first. Test/Behavoir-driven development(TDD/BDD) forces you to think about design/requirements before actually writting any code.

Today microservices and serverless make easier than ever to iterate quickly which means it too easy to introduce bugs and the technical debt quickly becomes unmanageble without the proper testing solution. Teams are increasingly becoming smaller and spread out. It is no longer feasible to use slack and email to ask the most basic questions about a service. A comprehensive test suite documents how a service is used at a high level.

## Stoplight Scenarios

We engineered Scenarios from the ground up to be:

* **Powerful** Easily assert, capture, transform, and validate your API Spec (OpenAPI) against your actual API. And if that isn’t enough, Prism has a powerful javascript runtime.

* **Portable** Scenarios are described in plain JSON with a well thought out, robust specification. Use our visual editor to quickly generate and manage this JSON. Scenarios can be run from our visual tooling, or completely outside of Stoplight, on your own machines, or on your continuous integration server.

* **Flexible** Your APIs, your tests, your way. Scenarios only test what you want them to. They have no opinion about your architecture (Monolithic vs Microservices), company structure (in house vs distributed), development lifecycle (production vs TDD), and your environment (development vs staging vs production).

* **Fast** Time can’t be slowed down, and we can’t give it back to you. Creating tests should be quick, and waiting for you tests to run shouldn’t feel like watching water boil. Scenarios are run concurrently for maximum speed - run hundreds of API requests and test assertions in seconds.

---

**Related**

* [Prism Introduction](../prism/overview.md)
* [Leveraging Open API](levergage-openapi.md)
* [Continuous Integration](continuous-integration.md)
* [Run Scenarios In Stoplight](run-test-stoplight.md)
