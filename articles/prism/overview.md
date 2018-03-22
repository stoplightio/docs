# Prism Introduction 

Prism is a performant, dependency free server, built specifically to work with web APIs. 

### Features 
- Act as a mock server, routing incoming requests to example repsonses, or dynamically generating examples on the fly. 
- Act as a transformation layer, manipulating incoming requests and outgoing responses. 
- Act as a validation layer, validating incoming requests and outgoing responses. 
- Contract test your APIs, given an OAS(Swagger 2) file. 
- Log all or a subset of traffic to configurable locations. 
- Extend existing APIs with new endpoints or capabilites. 
- Act as a system-wide proxy, blocking traffic to particular websites or endpoints. 

### Simplicity Redefined 
Run it anywhere. It runs on OS X, Windows, and Linux, with no external dependencies. It is a single, self-contained binary file, that you can easily run from your terminal with a single command.  

## Getting Started 

#### macOS and Linux 

```# Install Prism 
curl https://raw.githubusercontent.com/stoplightio/prism/master.install.sh | sh
```

#### Windows 
Download the appropriate binary from [here](https://github.com/stoplightio/prism/releases). Unzip the binary file, then navigate in your terminal to the folder where you extracted Prism. 

### Run a Simple Mock Server 
Prism understands OAS(Swagger 2), so let's get started by spinning up a quick mock server for the popular Petstore API. To do this, run the following command in your terminal: 

```# os x / linux
prism run --mock --list --spec http://petstore.swagger.io/v2/swagger.json

# windows 
path/to/prism.exe run --mock --list --spec http://petstore.swagger.io/v2/swagger.json
```

Here, you are using the "run" command to run a server based on the spec file passed in via the --spec argument. The spec location can be the filepath to a file on your computer, or the URL to a publicly hosted file. The mock argument tells Prism to mock all incoming requests, instead of forwarding them to the API host described in the spec file. The list argument is a convenience, and tells Prism to print out the endpoints in the spec on startup. 

Prism starts on port 4010 by default - try visiting ```http://localhost:4010/v2/pet/findByStatus``` in your browser. This is one of the endpoints described in the petstore spec you passed in. You'll notice that it returns an error about a required query string parameter "status". This is the automatic request validation at work! The swagger spec specifies that a query string parameter names "status" is required for this endpoint so Prism simulates a 400 response for you. Reload the page with a query string parameter, and you will see the dynamically generated mock response ```http://localhost:4010/v2/pet/findByStatus?status=available```.

Tada! With a single command you have started a validating, dynamically mocking version of the Swagger petstore API. 

### Run some Contract Tests

Prism consumes OAS(Swagger 2) files. OAS provides the contract for your API. If your OAS file contains the x-tests extension (generated automatically if you use the Stoplight app to manage your OAS and tests) then you can run tests with Prism.

Check out [this specification](https://goo.gl/jniYmw). If you scroll past all the regular OAS properties, you will notice a ```x-tests``` extension near the bottom of the file. Inside of that property, we have a few test cases defined. This OAS file, along with its tests, is managed in the Stoplight app (we export our API from within the app to produce this file). 

#### To Run the Contract Tests 
```
# os x / linux 
prism test --spec https://goo.gl/jniYmw

# windows
path/to/prism.exe test --spec https://goo.gl/jniYmw
```

You should see some nice output to your terminal detailing the tests and assertions that are run. These tests take our OAS contract and apply it to your API. They act as a sort of sync manager. 

> If a test fails, it means one of two things - your API is broken or, our OAS contract is out of date / incorrect 
