# Assertions

## What is an Assertion?
- An API test consists of a series of steps (these are sometimes HTTP requests) that can be executed collectively or individually.
- An assertion is a specification that indicates the expected outcome (response) to a request executed in a test.
- A test is unsuccesful if an assertion fails i.e. the actual outcome is not equal to the expected outcome
- You can create assertions for status codes, response time, reponse content, header values, etc.
- When you execute an assertion, you can determine the type of operation you want to perform with your expected outcomes.

## Comparison Logic Available in Scenarios
- equals
- greater than
- greater than or equals
- less than
- less than or equals
- no equal
- exists
- length equals
- contains
- validate pass
- validate fail

## Why
- Assertions are checked any time a test is executed.
- Assertions are used to detemine the state of a test (pass or fail).
- Assertions are ideal for discovering if an API satisfies stipulated objectives.

## Assertions in Scenarios
- Scenarios in Stoplight are grouped into collections. To create an assertion for a step in Scenarios, you need to create a collection and add your Scenarios to it.
