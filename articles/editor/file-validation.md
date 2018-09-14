# File Validation

File validation is the process of checking a file's syntax and structure to make sure it meets specific requirements. Stoplight's validation ensures file edits are in the correct format. This is especially helpful while editing structured file formats (e.g. OpenAPI documents) so that any errors can be resolved quickly and efficiently.

![File Validation](https://github.com/stoplightio/docs/blob/develop/assets/gifsv2/file-validation.gif?raw=true)

File validation is run after every file edit to make sure no errors were introduced. A notification will appear if validation errors were introduced so that they can be resolved before attempting to save. If a validation error is detected, an alert will appear with an explanation of the issue and where it occurred.

Validation failures come in two levels:

* **Warnings** - A warning is generated if the validation process found a non-critical issue that did not interrupt the processing of the document. As an example, inclusion of non-standard fields in an OpenAPI document will display as a warning.

* **Errors** - An error is generated if the validation process found a critical issue that prevented the processing of the document. As an example, not including the correct fields in an OpenAPI document will display as an error.

Different types of file validations are used throughout the Stoplight platform. At a high level, file validations aim to identify the following two groups of errors:

* **Syntax** - Most files stored in Stoplight are either JSON or YAML format, so they must always adhere to the JSON/YAML formatting standards. If anything typed into the editor does not meet the format criteria, it will be rejected with a notification pointing to where the syntax error occurred. _Syntax errors will prevent the file from being saved until all errors are resolved._

* **Correctness** - Certain files stored within Stoplight must adhere to high-level specifications to ensure they are able to be read and processed correctly. The OAS/Swagger specification is one such standard. It is critical that every OAS document stored in Stoplight meet these standards. If an error is detected in any document, either an error or warning will be generated with a description of the issue.

---

**Related Articles**

* [Validating Your API Spec](/modeling/modeling-with-openapi/validating-your-api-spec)
