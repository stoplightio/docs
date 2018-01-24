# Web & Desktop App

Stoplight has a desktop app! Download the appropriate version here (link).

## Web or Local?
The main difference between the Stoplight desktop app and the web app is that the desktop app can store requests and test data offline. It can also connect with APIs that are behind firewalls or otherwise not available on the public internet (localhost as well).

## Local Prism
When you start the Stoplight desktop app, it will start an instance of Prism on http://localhost:4010. This is same as if you downloaded the Prism binary, opened your terminal, and started prism manually. When you run local tests in the desktop app, it takes care of calling a local instance of Prism with the correct arguments and spec files.

## Local Save
* The Stoplight desktop app can read/write specification files on your local file system. This is perfect if you generate your specification outside of Stoplight (like from code), want to use version control systems like Git, or want to use your favorite IDE to work on the spec. 
* This feature is **NOT** available in the web app 


