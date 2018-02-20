# Continuous Integration with Jenkins

Integrating Prism into your [Jenkins](https://jenkins.io/) pipeline is easy.
There are two ways to get started with Jenkins:

* Running Prism in a pipeline step natively or using Docker
* Using the "Stoplight Report" Jenkins Plugin

## Adding Prism to a Pipeline

To get started, you will need to either install Prism natively on the Jenkins
system, or use the official [Stoplight Prism Docker image](https://hub.docker.com/r/stoplight/prism/).

When integrating Prism into a Jenkins pipeline, there are two different
approaches:

* Starting Prism in the background to act as either a mock or
  contract/validation server
* Having Prism conduct a scenario against a running server by running as a
  dedicated test step

### Running Prism in the Background

To run Prism in the background, you will need to start Prism prior to kicking
off your tests. If running natively, use the command format:

```sh
BUILD_ID=dontKillMe nohup prism mock --spec ... &
```

<!-- theme: warning -->

> Please note that the trailing ampersand (`&`) is required

If running in Docker, use the format:

```sh
docker run -d --rm -p 4010:4010 stoplight/prism:latest mock --spec ...
```

For more information on using Prism as a test server, see [here](./overview.md).

### Running Prism in the Foreground

To run Prism in the foreground, you will call Prism like you would any other
test step. If running natively, use the command format:

```sh
prism conduct ...
```

If running in Docker, use the format:

```sh
docker run --rm stoplight/prism:latest prism conduct ...
```

When running `prism conduct`, you can:

* Include the Scenario JSON on your CI server, and pass in its absolute file path
* Pass in the absolute URL to the scenario JSON served up via HTTP

<!-- theme: warning -->

> Don't forget to pass in any required environment values with the --env command
> line flag (or you can provide the filepath to a json file with your environment
> variables)!

<!-- theme: info -->

> Did you know? You can find the full command to run your scenario collection
> or individual scenarios in the Stoplight application. Click on the "Home"
> button of a scenario under "Trigger This Collection".

## Using the Plugin

Members of the Stoplight community were kind enough to create the [Stoplight
Report Plugin](https://github.com/jenkinsci/stoplightio-report-plugin), which is
a Jenkins plugin that can be used to run tests with Prism. For more information
on the plugin, see [here](https://plugins.jenkins.io/stoplightio-report).

---

**Related**

* [Jenkins Website](https://jenkins.io/)
* [Continuous Integration Overview](./continuous-integration.md)
* [Continuous Integration with Circle CI](./continous-integration-circle)
* [Continuous Integration with Travis CI](./continous-integration-travis)
* [Prism Docker Image](https://hub.docker.com/r/stoplight/prism/)
* [Stoplight Report Plugin Homepage](https://plugins.jenkins.io/stoplightio-report)
* [Stoplight Report Plugin Github](https://github.com/jenkinsci/stoplightio-report-plugin)
