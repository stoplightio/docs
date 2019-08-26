# Customize Style & Validation Rules

![Customize Style and Validation Rules](https://github.com/stoplightio/docs/blob/develop/assets/imagesv2/style-validation-rules.png?raw=true)

## What

In Stoplight Next you can customize the style and validation settings. This provides a practical method for enforcing API design rules over multiple APIs. You can enable or disable rules that monitor and validate things like your API, operations, markdown, parameters, paths, and references. Enabling a rule means our spec validator will trigger either a warning (denoted by a yellow exclamation icon) or an error (denoted by a red exclamation icon) if the rules conditions are not met.

### Style Rules

Style rules refer to non-OAS specific rules such as setting requirements around providing descriptions for operations. Style rules are denoted by a blue pencil icon and typically trigger warnings when enabled.

### Validation Rules

Validation rules refer to OAS specific rules that signify whether a specification is technically correct. An example of a validation rule would be requiring a unique `operationID` for every operation. Validation rules are denoted by a green check mark icon and typically trigger errors when enabled.

> The Style & Validation rule engine is powered by our open-source project [Spectral](https://github.com/stoplightio/spectral)

## How

1. Select the **Project** you would like to modify
2. Select the **lint** settings from the file explorer on the bottom left
   > The lint settings can also be accessed via the settings cog within the validation pane of the editor
3. Enable or disable rules by clicking the toggle next to the rule you wish to modify
4. Make sure to **save** your lint changes before exiting

---

**Related Articles**

- [Modeling Introduction](/modeling/introduction)
- [Using the CRUD Builder](/modeling/modeling-with-openapi/using-the-crud-builder)
- [API Operations](/modeling/modeling-with-openapi/api-operations)
- [API Models](/modeling/modeling-with-openapi/api-models)
- [Security Schemes](/modeling/modeling-with-openapi/security-schemes)
- [OAuth](/modeling/modeling-with-openapi/oauth)
- [Shared Parameters and Responses](/modeling/modeling-with-openapi/shared-parameters-and-responses)
- [Referencing Another API Spec](/modeling/modeling-with-openapi/referencing-another-api-spec)
- [Sending HTTP Requests](/modeling/modeling-with-openapi/sending-http-requests)
- [Validating Your API Spec](/modeling/modeling-with-openapi/validating-your-api-sec)
