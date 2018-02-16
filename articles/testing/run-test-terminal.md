# Running Prism from the Terminal

It is very easy to run scenario collections, or individual scenarios, on your own computer, completely outside of the Scenarios app.

First, install Prism, our command line tool for running scenarios.

_On macOS or Linux:_

```
curl https://raw.githubusercontent.com/stoplightio/prism/2.x/install.sh | sh
```

_On Windows:_

```
Download from https://github.com/stoplightio/prism/tree/2.x
```

After installing, you should be able to run `prism -h` (or `prism.exe -h` in Windows) from your CLI and see the Prism help text.

The Scenario app has a convenient display that gives you the exact command required to run the collection or scenario that you are viewing, taking into account your current environment variables. If you have the Scenario editor connected to a local file on your computer, it will use the path to that file, otherwise it will use the Scenario SRN (unique identifier).

<!-- theme: warning -->

> Keep in mind that if you are storing your Scenarios on Stoplight's servers, and running them from the command line, you must save them in the Stoplight app before running! This is because Prism will make a call to the Stoplight API to fetch your Scenario JSON, which it will then run from your computer.

See below for a screenshot of the "Run From Terminal" command generator. The command in this box will update live in response to environment, user, and scenario changes.

![](http://i.imgur.com/mqpNanE.png)

## Running Scenarios

To run a local Scenario, you can use the `prism conduct` command. The `conduct`
command accepts either a local file path or URL. If you are working with a local
Scenario `collection.json` file, you can run the Scenario using the following
command:

```bash
prism conduct /path/to/collection.json
```

For more information on Scenarios and how they can be used, see [here](./scenarios-introduction.md).

## Contract Testing

To use Prism for contract testing (or API validation), you can use the `prism validate` command.
The `validate` command takes a `--spec` argument, which is either a file path or URL to an OpenAPI specification file.
To run a contract test against the default API URL set in the specification, use the command:

```bash
prism validate --spec /path/to/my/spec.json
```

You can also run a contract test against a specific upstream URL with the
`--upstream` argument.

```bash
prism validate --spec /path/to/my/spec.json --upstream http://localhost:8080
```

For more information on contract testing and how it can be used, see [here](./contract-testing.md).

## Related

* [Scenarios Overview](./scenarios-introduction.md)
* [Contract Testing Overview](./contract-testing.md)
* [Integrating Prism into a CI Pipeline](./continuous-integration.md)
