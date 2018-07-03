# Versions

## What

Versions are editable snapshots of your current Project. When you create a new project, it will automatically start at version 1.0. You should create a new version within your project when you are ready to start working on large or "breaking" changes to your product. This allows for managing multiple projects, while still keeping the older ones available to edit. It is advisable to only have a few versions per project.

> Versions in Stoplight follow the [Semantic Versioning](https://semver.org/) number conventions and are marked by MAJOR.MINOR.

## How

1.  Select the **Project** you wish to modify
2.  In the top right, select the **Branch** icon with the version
    number

### Navigate to a Version

1.  The version you are currently viewing will be highlighted in blue in the tree
2.  Select any version nested under the code branch folders

### To Create a New Version

1.  Input a new Version Number, then click **+ Version **

    - Invalid formats are anything that include non-number character and will result in an error upon creation

2.  On successful creation of the new version, you will re-routed to it and you may continue working as normal, without concern of altering any work in other versions

> New versions will be generated from the nearest Version numerically lower than it

## Notes

Git branches are used internally to manage versions. Under the hood for each version, a branch is created as `version/{MAJOR.MINOR}`.

It is important to note that a change in a version release will only be refelected in itself and will not propagate to any other versions. As an example changing Version 1.0, after Version 2.0, is created, will NOT update Version 2.0 in anyway.

---

**Related Articles**

- [Versioning & Releases](./introduction.md)
- [Releases](./releases.md)
- [Read, Design, & Code View](/platform/editor-basics/read-design-code-view)
- [Working with Files](/platform/editor-basics/working-with-files)
- [Import Files](/platform/editor-basics/import-files)
- [Export Files](/platform/editor-basics/export-files)
- [Change History](/platform/editor-basics/change-history)
- [Editor Configuration](/platform/editor-basics/editor-configuration)
- [Environments](/platform/editor-basics/environments)
- [File Validation](/platform/editor-basics/file-validation)
