# Dynamic Mocking 

![Dynamic Mocking](https://github.com/stoplightio/docs/blob/develop/assets/imagesv2/dynamic-mocking.png?raw=true)

## What 
By default, when a request comes into Prism (if the method and path are found in your specification) then the lowest response is mocked back. If there is an example, then it will be mocked back, otherwise, a response will be generated for you. You can force dynamic mocking even if you have an example response by following these steps. 

## How 
1. Select the testing file you want to dynamically mock 
2. Select **Query** under Send Test Requests 
3. Click **Add Query**
4. Input ```__dynamic``` for query name 
5. Input ```true``` for query value 

---
**Related Articles**
- [Mocking Introduction](/mocking/introduction)
- [Javascript Runtime](/mocking/javascript-runtime)
