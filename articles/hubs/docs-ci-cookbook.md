# API Documentation CI Cookbook

This document covers publishing API documentation directly from the Stoplight
API. The steps provided below cover:

- [Updating a file](#updating-a-file) - if you generate your API specifications
  from code, you can use the request outlined below to programmatically update
  the file stored in Stoplight

- [Retrieving doc IDs for a project](#retrieving-doc-ids-for-a-project) - you'll
  need to retrieve the "doc ID" for your project in order to know which ID to
  publish under.

- [Publishing a build](#publishing-a-build) - once you've retrieved the doc ID,
  you can publish a build under a provided domain and optionally set it live in
  one API call.

- [Downloading a build](#downloading-a-build) - once the build is completed, you
  can download the static contents of the generated output for serving locally
  or hooking into another content pipeline.

### Prerequisites

Prior to continuing, you'll need:

- A valid Stoplight API access token -
  https://next.stoplight.io/profile/access-tokens

- Within the Stoplight UI, create a domain and test build using the project
  [publish interface](https://docs.stoplight.io/documentation/publishing)

  > Be sure to set the appropriate settings, file, and configuration for the
  > published documentation. You only need to set them once in the UI in order
  > to use them programmatically from the API.

- The project ID of the project you will be updating. The ID of a project can be
  found in the project settings interface.

## Updating a File

To update an existing file in Stoplight:

```bash
# the project to update
PROJECT_ID="123"

# the location of the file in stoplight (NOTE, all OAS files in
# Stoplight the '.yml' extension, even though we are writing in
# JSON)
TARGET_FILE_NAME="main.oas2.yml"

# the target branch in Stoplight to write to
TARGET_BRANCH="version/1.0"

# the location of the JSON file on the local filesystem
SOURCE_FILE_PATH="./my-spec.json"

# the stoplight API access token
ACCESS_TOKEN="..."

curl \
    -XPUT -H 'Content-Type: application/json;charset=UTF-8' \
    -H "Authorization: Bearer $ACCESS_TOKEN" \
    --data-binary "{ \"content\": $(cat $SOURCE_FILE_PATH), \"branch\": \"$TARGET_BRANCH\", \"commit_message\":\"Updating $TARGET_FILE_NAME\" }" \
    "https://next-api.stoplight.io/projects/${PROJECT_ID}/files/${FILE_NAME}" \
    --compressed
```

> Note, the `Content-Type` header is very important.

## Retrieving Doc IDs for a Project

You can verify a documentation domain is ready for publishing by issuing a
request against the `/docs.list` endpoint:

```bash
# the project to update
PROJECT_ID="123"

# the stoplight API access token
ACCESS_TOKEN="..."

curl \
    -XGET -H 'Content-Type: application/json;charset=UTF-8' \
    -H "Authorization: Bearer $ACCESS_TOKEN" \
    "https://next-api.stoplight.io/docs.list?projectId=$PROJECT_ID" \
    --compressed
```

> **IMPORTANT** Be sure to take note of the `id` key in returned `docs` array
> for the domain you want to publish under. You'll need it later on.

## Publishing a Build

You can publish a build using the `/docs.release` endpoint:

```bash
# the doc to update (retrieved from the section above)
DOC_ID="456"

# the stoplight API access token
ACCESS_TOKEN="..."

curl \
    -XPOST -H 'Content-Type: application/json;charset=UTF-8' \
    -H "Authorization: Bearer $ACCESS_TOKEN" \
    --data-binary '{ "setLive": true }' \
    "https://next-api.stoplight.io/docs.release?id=$DOC_ID" \
    --compressed
```

> **NOTE** by setting the `setLive` to `true` in the request body, the build
> will automatically be made live. Use `setLive` as `false` if you only want to
> build, but not publish.

> **ALSO NOTE** If you want to download the build you just generated, take note
> of the response `build.id` value. You'll need it in the following step.

If you are hosting documentation with Stoplight, then you are done! Once the
build is completed and published, your documentation visitors will automatically
see the latest version.

## Downloading a Build

You can download the static contents (HTML, CSS, JS) of a published build using
the `/docs.release` endpoint:

```bash
# the build ID to download (retrieved from the section above)
BUILD_ID="789"

# the stoplight API access token
ACCESS_TOKEN="..."

curl -o build.zip \
    -H "Authorization: Bearer $ACCESS_TOKEN" \
    "https://next-api.stoplight.io/docs.builds.download?id=$BUILD_ID"
```

The static contents of the rendered documentation are now located in the
`build.zip`.
