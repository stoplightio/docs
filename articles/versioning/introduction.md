# Versioning and Release

You can declare Versions and Releases within Stoplight to manage and track changes made to your Project over time. You can identify which version you are viewing in the top right of the editor. Versions will be marked with a **Branch** icon, while releases will be marked with a **Tag** icon. Stoplight partially follows the [Semantic Versioning](https://semver.org/) numbering conventions of MAJOR.MINOR.PATCH, using only major and minor.

- Major Version: When large incompatible breaking changes have been made
- Minor Version: When backwards-compatible functionality have been added

### Versions

Versions are editable snapshots of your current Project. When you create a new Project, it will automatically start at version 1.0. [More on Versions...](./versions.md)

### Releases

Creating a Release marks a version as ready to publish and takes a time stamped snapshot of a the most recent edit of a version. When publishing all released versions will be included in your documetation under a dropdown selector [More on Releases...](./releases.md)

## Best Practices

Depending on the focus of your project, we recommend following different versioning patterns for the best workflow experience within Stoplight. For example, if your project's primary focus is documentation you may want to use a different approach than if the focus is modeling out an API, but feel free to use whatever pattern you feel works best for your team!

### Product/API Release Cycle

The simpliest and most common approach is to mirror your product or APIs release cycle. The basic rule of thumb is when you release a new version of your API, you create a new release in Stoplight under the same version number. This release flow is one-to-one with your API, and will usually result in a large number of releases within Stoplight.

### Platform Versions

If you are creating a documentation driven project, you can describe the major versions of your platform via versioning. This will allow you to document multiple versions of your platform under one domain. In this use case, it is not necessary to use releases.

## Icons and Tooltips

- Solid Upload: A released Version
- Outlined Upload: A Version that has not yet been released
- Code: A sorted folder of versions of the same MAJOR

---

**Related Articles**

- [Versions](./versions.md)
- [Releases](./releases.md)
- [Read, Design, & Code View](/platform/editor-basics/read-design-code-view)
- [Working with Files](/platform/editor-basics/working-with-files)
- [Import Files](/platform/editor-basics/import-files)
- [Export Files](/platform/editor-basics/export-files)
- [Change History](/platform/editor-basics/change-history)
- [Editor Configuration](/platform/editor-basics/editor-configuration)
- [Environments](/platform/editor-basics/environments)
- [File Validation](/platform/editor-basics/file-validation)
