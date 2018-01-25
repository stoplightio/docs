# Setting Up a Prism Mock Server

Mock servers are great for quickly standing up a fake (sometimes referred to as virtualized) version of your web service. Amongst other things, you can use mock servers to:

1. **Parallelize and speed up development.** Frontend teams can build against the mocked API while the backend team implements the real API.
2. **Increase the accessiblity of your API.** Customers can build implementations on top of your API before committing to a paid account.
3. **Make testing easier.** APIs (particularly microservices) usually make calls to other APIs. Those other APIs might in turn make calls to even more APIs. This creates a dependency chain nightmare. During testing, you can use mock servers to cut that dependency chain off at the start.

If you are coming from Stoplight Classic (Version 2), you will notice that there is a little bit more setup involved.

## Hosted Mock Server Steps

_Note: We plan to introduce templates to the Stoplight editor file creation process soon. This feature will automate most of the steps below, and turn mock server creation into a one-click solution._

1. Create a **new Stoplight project**.
2. Inside of your new project, create a **OAS (Swagger 2) modeling file**. Let's name it `hello.oas2`. You can learn more about our visual OAS editor here.

![](//s3.amazonaws.com/hifs/mock/hello.oas2.gif)

3. Add a `GET /hello` operation to your new OAS specification.
4. Add a **200 response** to the operation, with the example JSON described below. **Save** the OAS file.

```json
{
  "mock": "api"
}
```

![](//s3.amazonaws.com/hifs/mock/get.hello.200.gif)

5. Create a new **Prism instance file** in the project. Name it `hello-mock.prism`.
6. Prism instances are made up of APIs and Rules, you can learn more about them here. Add an API to the Prism instance, and connect the `hello.oas2` specification that you created earlier.

![](//s3.amazonaws.com/hifs/mock/hello.prism.api.gif)

7. Next, add a **new rule** that you will setup to power the mocking. Rules simply apply scenarios to HTTP traffic passing through the Prism instance.
8. Once you have created a new rule, you need to connect it to the API we added earlier. To do that, click on the `apis` dropdown input, and select the previously created API.
9. Finally, you need to add a **scenario** that will actually perform the mocking. We have an official Stoplight mock scenario [here](https://next.stoplight.io/stoplight/prism?edit=%23%2Fscenarios%2Fmock), which makes it easy to get started. Add a scenario to the `before` section of your rule. Select `another project` in the first dropdown, and then search for `prism`. The file in that project you are looking for is `helpers.prism.yml`, and the specific scenario is called `mock`. This mock scenario should suit most of your mocking use cases. For advanced use cases please send us a message and we would love to help out.

![](//s3.amazonaws.com/hifs/mock/hello.prism.rule.gif)

8. **Save** your Prism instance. To verify that your mock server is working, click on the `Home` link at the top of the prism instance sidebar, and then send a test request to `GET /hello`. You should see a 200 response that equals the example you set in your OAS file earlier!

![](//s3.amazonaws.com/hifs/mock/hello.prism.gif)

# Running Your Prism Server Locally

In the previous section, you learned how to create a simple Prism instance that is hosted with Stoplight. It is a powerful, accessible tool that allows your frontend and backend teams to work simultaneously. But the hosted prism instance might not work behind your company firewall, or you might want to run Prism locally on your desktop. Well you are in luck, prism is easy to install and run.

## Local Mock Server Steps

1. Install [Prism](https://github.com/stoplightio/prism). Make sure to install Prism Next, the version should be >= `2.0.0-beta.x`.
2. Open up your terminal and log into Stoplight Next with the `prism login` command, and enter your Stoplight Next credentials. Once you are logged in, you will have access to your private and all public projects.
3. Get the export link for the prism mock instance you created above.
4. Run `prism serve {export-link} --debug` and open this [link](http://localhost:4010/helloWorld).

![](//s3.amazonaws.com/hifs/mock/hello.prism.local.gif)

# Recap

You now have a fully functional prism mock server. We have created a public project full of useful prism resources. We encourage you to explore the other prism helpers which are located [here](https://next.stoplight.io/stoplight/prism/blob/master/helpers.scenarios.yml). Let us know what you think, we are excited to see what you do.

For the more experienced Prism user, we have set up some advanced prism instances in the official Stoplight Next [Prism Project](https://next.stoplight.io/stoplight/prism).
