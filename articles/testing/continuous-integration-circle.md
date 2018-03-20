# Continuous Integration with CircleCI

Integrating Prism into your Circle CI pipeline is easy. The simplest way to get
up and running is by using [Stoplight's Prism Docker
image](https://hub.docker.com/r/stoplight/prism/).

To get started, you will need to reference the Prism Docker image in the
`docker` section of either the `build` or `test` sections of your Circle CI
configuration file. This file is typically located under the `.circleci`
directory in the root of your repository.

When integrating Prism into a CircleCI pipeline, there are two different
approaches:

* Starting Prism in the background to act as either a mock or
  contract/validation server
* Having Prism conduct a scenario against a running server by running as a
  dedicated test step

## Running Prism in the Background

Below is a sample Circle CI configuration file (version 2) using Prism as a
mock or contract/validation server:

```yaml
version: 2
jobs:
  build:
    docker:
      # The first image is where your commands will be run,
      # so be sure that the prism image is not first
      - image: your-normal-image:your-version
      # Customize the 'command' to fit your needs.
      - image: stoplight/prism:latest
        command: [prism, ...]
    steps:
      # Run test suite against http://localhost:4010
      ...
```

Once the Prism container is started, it will automatically start listening on
`http://localhost:4010` for any open connections.

## Running Prism in the Foreground

Below is a sample Circle CI configuration file (version 2) with
Prism conducting a scenario:

```yaml
version: 2
jobs:
  build:
    docker:
      - image: your-normal-image:your-version
    steps:
      - checkout
      - run:
          name: Install prism
          command: curl https://raw.githubusercontent.com/pytlesk4/stoplight-todos/master/prism.sh | sh
      - run:
          name: Start your service
          command: ...
          background: yes
      - run:
          name: Run scenario
          command: prism conduct ...
      ...
```

When running `prism conduct` you can:

* Include the Scenario JSON on your CI server, and pass in its absolute file path
* Pass in the absolute URL to the scenario JSON served up via HTTP

> Don't forget to pass in any required environment values with the --env command
> line flag (or you can provide the filepath to a json file with your environment
> variables)!

> Did you know? You can find the full command to run your scenario collection
> or individual scenarios in the Stoplight application. Click on the "Home"
> button of a scenario under "Trigger This Collection".

---

**Related Articles**
- [Integrating in Continuous Integration](/testing/continuous-integration/overview)
- [Integrating with Jenkins](/testing/continuous-integration/jenkins)
- [Integrating with Travis](/testing/continuous-integration/travis)
- [Prism Docker Image](https://hub.docker.com/r/stoplight/prism/)
