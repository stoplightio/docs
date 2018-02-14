# Running a Scenario from Terminal

It is very easy to run scenario collections, or individual scenarios, on your own computer, completely outside of the Scenarios app.

First, install Prism, our command line tool for running scenarios.

*On macOs or Linux:*
```
curl https://raw.githubusercontent.com/stoplightio/prism/2.x/install.sh | sh
```

*On Windows:*
```
Download from https://github.com/stoplightio/prism/tree/2.x
```

After installing, you should be able to run `prism -h` (or `prism.exe -h` in Windows) and see some help text. 

The Scenario app has a convenient display that gives you the exact command required to run the collection or scenario that you are viewing, taking into account your current environment variables. If you have the Scenario editor connected to a local file on your computer, it will use the path to that file, otherwise it will use the Scenario SRN (unique identifier).

<!-- theme: warning -->
> Keep in mind that if you are storing your Scenarios on Stoplight's servers, and running them from the command line, you must save them in the Stoplight app before running! This is because Prism will make a call to the Stoplight API to fetch your Scenario JSON, which it will then run from your computer.

See below for a screenshot of the "Run From Terminal" command generator. The command in this box will update live in response to environment, user, and scenario changes.

![](http://i.imgur.com/mqpNanE.png)

## Running Local Files

The `prism conduct` command accepts a filepath. So, if you are working with [local scenario collection](#docTextSection:Ap4Z2B7RgbbLFLjJD) .json files, you can run them with something like:

```bash
prism conduct /path/to/collection.json
```

## Including Specs For Contract Testing

If you are using [contract testing](#docTextSection:tFWniZdshJYLLtKms), you will need to include the filepath to the API specification as part of the command. This is what that looks like:

```bash
prism conduct myOrg/scenarios/myScenarios --spec /path/to/my/swagger.json
```

## Continuous integration

Most CI products (Circle CI, Travis, Jenkins, Codship, etc) generally function in the same way: setup environment, invoke commands to run tests. With Scenarios + Prism, the process is similar. Install Prism, and then configure the CI process to run the appropriate Prism command. We've included instructions for Circle CI below, but these concepts should loosely apply to other CI products.

#### Circle CI

Integrating [Prism](http://stoplight.io/platform/prism) into Circle CI is easy. All you need to do is install Prism and overide the test command.

To install Prism just add a dependency to your circle config.


``` yaml
dependencies:
  pre:
    - curl https://raw.githubusercontent.com/stoplightio/prism/2.x/install.sh | sh
```


Then override the default test command for circle in your config.


``` yaml
test:
  override:
    - prism conduct orgId/scenarios/scenarioId
```

When running `prism conduct` you can:

- Use the Scenario SRN, as displayed above.
- Include the Scenario JSON on your CI server, and pass in its absolute file path
- Pass in the absolute URL to the scenario JSON served up via HTTP.

<!-- theme: warning -->
> Don't forget to pass in any required environment values with the --env command line flag (or you can provide the filepath to a json file with your environment variables)!

For convenience, you can find the full command to run your scenario collection or individual scenario in the Stoplight app.
