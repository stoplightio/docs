# Sending HTTP Requests

<!---Gif of simple request plus extending spec--->

## What

Use the HTTP Request Maker to send requests to the endpoints defined in your specification, extend your specification with new endpoints, or send a request to any endpoint.

## How

1.  Click **HTTP** in the top tool bar located above the editor.
2.  Select a **method** from the first dropwdown.
3.  Choose a **path** from the next dropdown, or enter any **valid API endpoint**.
4.  If the variables tab is present, fill in any required values
5.  Use the tabbed menu to add headers, query params, request body information, or authentication.
6.  Click **send** and view the results.

> #### Bonus
>
> Click **Extend Spec** to append or alter your specification using the information supplied in the request maker.

## Additional Notes

* The Code Generation tab can but used to view your request in another language so it can be sent through other means.

* If a path or endpoint is selected from your current specification, the tabbed menu will prepopulate with any parameters defined in the spec.

* To add variable path parameters, wrap the parameter name in the path in curly braces like so `/path/{param}` and then fill in the value in the Variables tab.

* To use environment variables in your request, enter `{$$.env.variable_name}` as the value and the populated value can be viewed or changed in the variables tab.

---
**Related Articles**
[Using Environment Variables](/testing/using-variables/environment)
