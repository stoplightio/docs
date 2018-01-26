# Setting up a Hosted Prism Contract Server

Contract servers are a powerful tool in a developer's toolbox. They use your OAS (Swagger 2) and JSON Schema definitions to validate HTTP traffic passing through your API. You can use them to:

1. **Add Contract Tests to an Existing Test Suite**
    - Already have a test suite? No problem! Point your tests at the contract test server, and it can annotate responses with the contract test results. Your test suite just has to check for these response headers and fail appropriately.
2. **Monitor Traffic for Anomalies** 
    - Know _when_ your implementation breaks instantly, and _why_. By sending all your traffic through your contract server, you can flag that 1 in 1000 request anomaly.
3. **Detect Changes in 3rd Party APIs** 
    - APIs (particularly microservices) usually make calls to other APIs. These dependencies can be disconcerting because you have no control over when they change. With contract servers positioned between you (the consumer) and the external API, you can be alerted when the external API changes.

> **Real World Use Case** - Still not convinced, then head on over to Sendgrid and learn how they used contract servers to power their [integration tests](https://sendgrid.com/blog/stoplight-io-to-test-api-endpoints) for their 7 SDKs.

If you aren't familiar with JSON Schema, we highly recommend you head [here](https://spacetelescope.github.io/understanding-json-schema/) first.

If you are coming from Stoplight Classic (v2), you will notice that there is a little bit more setup involved, but  only a couple steps.

## Hosted Contract Server Steps

_Note: We plan to introduce templates to the Stoplight editor file creation process soon. This feature will automate most of the steps below and turn mock server creation into a one-click solution._

_For this article we will validate a service that already exists. It is just a simple API representing a todos list manager that is running at http://todos.stoplight.io. We have created an OAS Specification for it already and you can download it [here](https://exporter.stoplight.io/3351/master/todos.oas2.yml)._

1. Let's create a new project, create a new spec, name it `todos.oas2`, and paste the JSON from the spec above in the code editor.

![](../../assets/gifs/validation-todos-contract-guide.gif)

2. Create a new **Prism instance file** in the project. Name it `todos.contract.prism`.
3. Prism instances are made up of APIs and Rules, you can learn more about them here. Add an API to the Prism instance and connect the `todos.oas2` specification that you created earlier. Also, let's change the `id` to `todos` and set the _Upstream URL_ to _http://todos.stoplight.io_. The Upstream URL is where the contract server will forward incoming requests.

![](../../assets/gifs/validation-todos-prism-api.gif)

4. Next, add a **new rule** that you will setup to power the validation. Rules simply apply scenarios to HTTP traffic passing through the Prism instance.
5. Once you have created a new rule, you need to connect it to the API we added earlier. To do that, click on the `apis` dropdown input and select the previously created API. Connecting the rule to the API you defined earlier makes the OAS file available to scenarios in the rule.
6. Lastly, you need to add a **scenario** that will actually perform the validation. We have an official Stoplight validate scenario [here](https://next.stoplight.io/stoplight/prism?edit=%23%2Fscenarios%2validate), which makes it easy to get started. 
    1. Add a scenario to the `after` section of your rule. 
    2. Select `another project` in the first dropdown.  
    3. Search for `prism`. 
        1. The file you are looking for within that project is `helpers.prism.yml` and the specific scenario is called `validate`. 
        
This validate scenario should suit most of your needs. It will check the request/response headers, request/response body, request path parameters, and query strings. It will also add response headers to the HTTP request on the way back to the consumer with the results of the validation. For advanced use cases, please send us a [message](). We would love to help out!

![](../../assets/gifs/validation-todos-prism-rule.gif)

7. Save and let's verify that your contract server is working. Click on Home and let's Send a Test Request to `GET /todos`.

_Stoplight's visual editior makes it really easy to debug reqeust/response. If look at the response headers, specifically `Sl-Valid` , it should be `false`. This signifies that (according to your API specification) the request/response isn't valid, aka the contract test failed. You can find out why by inspecting the `Sl-Validation-Messages`. For the purpose of this article, the messages are below, and it looks like user is a required property and it is missing._

```js
// Sl-Validation-Messages
[
  {
    response: {
      message: "The document is not valid. see errors",
      error:
        "user: user is required\n0: Must validate all the schemas (allOf)\nuser: user is required\n1: Must validate all the schemas (allOf)\nuser: user is required\n2: Must validate all the schemas (allOf)\nuser: user is required\n3: Must validate all the schemas (allOf)\nuser: user is required\n4: Must validate all the schemas (allOf)\nuser: user is required\n5: Must validate all the schemas (allOf)\nuser: user is required\n6: Must validate all the schemas (allOf)\nuser: user is required\n7: Must validate all the schemas (allOf)\nuser: user is required\n8: Must validate all the schemas (allOf)\nuser: user is required\n9: Must validate all the schemas (allOf)\n"
    }
  }
];
```

![](../../assets/gifs/validation-todos-prism-verify.gif)

8. Let's get rid of this validation error. We don't have control over the API implementation so we have to update our specification.
9. Navigate to the `todos.oas2` file, update the `Todo Full` by deleting the user property, and hit save.
10. Let's resend a request to `GET /todos` and inspect the results. This time `Sl-Valid` is `true`. Awesome, we now have a valid spec and API.

![](../../assets/gifs/validation-todos-prism-done.gif)

# Running your Prism Server Locally

In the previous section, you learned how to create a simple Prism instance that is hosted with Stoplight. It is a powerful, accessible tool that allows your frontend and backend teams to work simultaneously. But, the hosted prism instance might not work behind your company firewall or you might want to run Prism locally on your desktop. Well, you are in luck, Prism is easy to install and run.

## Local Contract Server Steps

1. Install [Prism](https://github.com/stoplightio/prism). Make sure to install Prism Next, the version should be >= `2.0.0-beta.x`.
2. Open up your terminal, log into Stoplight Next with the `prism login` command, and enter your Stoplight Next credentials. Once you are logged in, you will have access to your private and all public projects.
3. Get the export link for the prism mock instance you created above.

![](../../assets/gifs/prism-install.gif)

4. Run `prism serve {export-link} --debug` and open this [link](http://localhost:4010/todos). You can inspect the results by opening the developer console for your browser.

![](../../assets/gifs/validation-todos-prism-local.gif)

# Validating Mock Servers

Validating an existing service is powerful, but what happens if you are still implementing your API and all you have is a mock server? How do you keep the examples valid?

_Note: If you don't have an existing mock server, check out [this](https://next.stoplight.io/stoplight/stoplight-next-docs/blob/master/prism.mock.server.md) article first and then continue reading._

## Steps

1. Repeat step 7 above. That is it. Know you will know when your examples are out of date, not only will your mock server be accurate, but this can help you catch any errors in examples in your documentation that you provide to users.

# Recap

You now have a fully functional prism contract server. We have created a public project full of useful prism resources. We encourage you to explore the other prism helpers which are located [here](https://next.stoplight.io/stoplight/prism/blob/master/helpers.scenarios.yml). Let us know what you think, we are excited to see what you do.

For the more experienced Prism user, we have set up some advanced prism instances in the official Stoplight Next [Prism Project](https://next.stoplight.io/stoplight/prism).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI2NjI2NTU0OF19
-->