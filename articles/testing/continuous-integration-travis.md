# Continuous Integration with Travis CI

Integrating Prism into your Travis CI pipeline is easy. The simplest way to get
up and running is by using [Stoplight's Prism Docker
image](https://hub.docker.com/r/stoplight/prism/). 

To get started, you will need to make sure the `docker` service is listed under
the `services` section of your `.travis.yml` file.

When integrating Prism into a Travis CI pipeline, there are two different
approaches:

* Starting Prism in the background to act as either a mock or
  contract/validation server
* Having Prism conduct a scenario against a running server by running as a
  dedicated test step (ie, added to the `script` section)

## Running Prism in the Background

Below is a sample Travis CI configuration file using Prism as a mock or
contract/validation server:

```yaml
services:
    - docker

before_install:
    # start the mock server in the background
    - docker run -d -p 127.0.0.1:4010:4010 stoplight/prism mock ...
```

Once the Prism container is started, it will automatically start listening on
`http://localhost:4010` for any open connections.

## Running Prism in the Foreground

Below is a sample Travis CI configuration file with Prism conducting a scenario:

```yaml
services:
    - docker

script:
    - docker run --rm -it stoplight/prism conduct ...
```

When running `prism conduct` you can:

* Use the Scenario SRN
* Include the Scenario JSON on your CI server, and pass in its absolute file path
* Pass in the absolute URL to the scenario JSON served up via HTTP.

<!-- theme: warning -->
> Don't forget to pass in any required environment values with the --env command
line flag (or you can provide the filepath to a json file with your environment
variables)!

<!-- theme: info -->
> Did you know? You can find the full command to run your scenario collection
or individual scenarios in the Stoplight application. Click on the "Home"
button of a scenario under "Trigger This Collection".

***

**Related**

* [Continuous Integration Overview](./continuous-integration.md)
* [Continuous Integration with Circle CI](./continous-integration-circle)
* [Continuous Integration with Jenkins](./continous-integration-jenkins)
* [Prism Docker Image](https://hub.docker.com/r/stoplight/prism/)
