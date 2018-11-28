# Mocking FAQs

## Why is my mock sever failing?

- Mock server, powered by Prism, isn't configured properly.
  - [Learn more here](/mocking/introduction)
    - Make sure you connected your specification correctly.
    - Make sure before and after rules are set up correctly, we recommend using the Stoplight Shared/Common scenarios.

- Invalid specification. Please see your specification validation errors at the top right when viewing your specification.
  - [Learn more here](/modeling/modeling-with-openapi/validating-your-api-spec)

- Stoplight project is private, login with your Stoplight credentials.

  *Command line only*

  - From your favorite command line tool run `prism login`, then retry starting your Prism mock server.

- Email us at [support@stoplight.io](mailto:support@stoplight.io) or message us in Intercom, if the above solutions don't help.

  *Please include a link to your mock server instance with an example request that is failing.*
