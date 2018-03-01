# Sending HTTP Requests

# PUT GIF HERE

## What

Use the HTTP Request Maker to send requests to the endpoints defined in your specification, extend your specification with new endpoints, or send a request to any endpoint.

## Where

Navigate to the modeling editor by clicking one of your oas files in the project file tree. Then click "HTTP" in the top tool bar located above the editor.

## How

1.  Choose one of the supported HTTP methods
2.  Select a path from the next dropdown, or any valid API
3.  If the variables tab is present, fill in any required values
4.  Use the tabbed menu to add headers, query params, request body information, or authentication
5.  Click send and view the results

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Bonus**

6.  Click "Extend Spec" to append or alter your specification using the information supplied in the request maker

## Additional Notes

* The Code Generation tab can but used to view your request in another language so it can be sent through other means

* To add variable path parameters wrap the parameter name, in the path, in curly braces like so `/path/{param}` and then fill in the value in the Variables tab

* To use environment variables in your request, enter `{$$.env.variable_name}` as the value and the populated value can be viewed or changed in the variables tab
