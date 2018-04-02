# Variables in Hubs 

## What 

Inputting variables in API documentation whenever you consume them can quickly become a tedious time sink. Stoplight removes this obstacle by storing variables in your local browser. Once you input a variable, it populates the rest of your docs, no duplication, no problems. 

## How

You can specify variables in your docs by adding them at the specification level or directly into Hubs. 

### Modeling Method 

![Security Scheme in Specification](https://github.com/stoplightio/docs/blob/develop/assets/images/hubs-variables-modeling.png?raw=true)

1. Select the modeling file you wish to modify 
2. Create a new **security scheme** 
    1. Input a **key** (required, must be unique in this specification) 
    2. Select a **type** of security scheme 
    3. Select a location for the security scheme under **in**
    4. Input a **name** 
3. Reference the specification in your Hub

### Hubs Method 

![Adding variables to HTTP Request Maker](https://github.com/stoplightio/docs/blob/develop/assets/images/hubs-variables-hubs.png?raw=true)

1. Select the Hub you wish to modify 
2. Create a **HTTP Request Maker** block 
3. Select the **Headers** tab 
4. Click **Add Header** 
5. Input a **header name**
6. Input a **header value** 
