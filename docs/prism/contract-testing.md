# Contract Testing at Runtime 

## What 

The purpose of this document is to explain how to do contract testing with Stoplight at runtime.

Prism is a local service that can run behind your firewall which can - based on a valid OAS 2 Swagger file - contract test the following:
- Request & Response Bodies
- Request & Response Headers

## Requirements 

### Make sure you can download and install Prism binary on a machine behind your firewall
1. [Download Prism](https://github.com/stoplightio/prism)
2. Run prism validate -help from the command line to ensure installation of Prism was successful 
3. Example Command: 
```
prism validate --spec "location on disk of the internets" 
--upstream api to forward requests to defaults to what is defined in your specification" 
```
```
--debug to see logs
```
```
--port to change Prism's default port
```
### You will need an OAS2/ Swagger 2 specification file. This file contains the following necessary information:
1. Upstream service URL to be called defined in the specification 
2. Definition of request/response models being contract tested 

## How 

1. Start a local PRISM contract test server on a machine behind your firewall
> Inputs to this server are the Swagger / OAS 2 file you want to contract test
2. Configure your test suite to point to the host/port of the Prism Service
3. Run your tests which will:
> test->prism host:port->calls service URL defined in OAS 2 specification->response from service is contract tested against the response model defined in the OAS 2 file and result added to the header ->test
4. The test  which made the call will then inspect the header(s) to determine if the contract test succeeded or failed

![]()

> Sl-Request-Validation-Messages would be present if contract testing failed


