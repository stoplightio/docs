# Using Custom Validations

Behind the Stoplight API design interface is
[Spectral](https://github.com/stoplightio/spectral), Stoplight's open source
validation engine. Spectral was built from the ground up to be fast, easy-to-use, and, most importantly, extensible. This article discusses how to customize the rules that power Spectral for your own purposes, including how to create your own rules.

## Accessing Your Project's Git Repository

Before you can update the validation rules for a Stoplight project, you will
first need to [clone your project repository](/platform/projects/git-repo) using
git. Once cloned, you should see a `lint.yml` file within the repository
contents.

```bash
$ ls -l
total 64
-rw-r--r--  1 user  user   821 Jun 26 10:49 lint.yml
[...]
```

## Modifying the Validation Configuration

The `lint.yml` configuration file is what the API design interface uses for
determining what rules to apply to the specifications within a project.

The lint configuration has a root object `rules`, with two possible formats to
apply the rules to: `oas2` (for OpenAPI v2) and `oas3` (for OpenAPI v3). For
example, to set a custom OpenAPIv2 rule you would start with:

```yaml
rules:
  oas2:
    my-custom-rule: [...]
```

Where `my-custom-rule` is the key for the new rule, which will contain the
contents of the rule. The contents of the rule object can vary depending on the rule's `function` member.

As a simple example, let's say we want to ensure that a special spec extension
`x-partner-segment` is present in all of our OpenAPI v2 APIs. To enforce this,
we'll create a `truthy` function rule, which ensures that a value is present and
is equal to a non-empty string. This is what our rule would look like:

```yaml
rules:
  oas2:
    contains-partner-extension:
      enabled: true
      summary: The API has a `x-partner-segment` extension set.
      type: "style"
      given: "$"
      then:
        field: x-partner-segment
        function: truthy
```

Where:

- `enabled` dictates whether the rule is enabled by default. By setting it to
  `true`, it will be enabled on project load.

- `summary` is the summary of the rule that will display in the Stoplight user
  interface when the rule is violated.

- `type` can be equal to either `style` or `validation`

- `given` is the
  [JSONpath](https://goessner.net/articles/JsonPath/index.html#e2) to the
  elements in the API specification that we want to operate on. The `$` equals
  the root of the object, which is where we want our extension to be set

- `then` is the function definition itself, which takes a `function` (`truthy`).
  The `truthy` function then takes a `field` parameter, which is what we want to
  evaluate as "truthy" or not (`x-partner-segment`). Different functions take
  different parameters, so be sure to check the latest Spectral documentation
  for the latest function parameters.
