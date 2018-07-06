# Versioning and Releases

![Versioning](https://github.com/stoplightio/docs/blob/develop/assets/images/stoplight-versioning.png?raw=true)

You can declare Versions and Releases within Stoplight to manage and track changes made to your Project over time. You can identify which version you are viewing in the top right of the editor. Versions will be marked with a **Branch** icon, and will have a **Solid Upload** icon if it has been released. Stoplight uses the numbering system: v{MAJOR.MINOR}

- Major Version: When large incompatible breaking changes have been made
- Minor Version: When backwards-compatible functionality have been added

### Versions

Versions are editable snapshots of your current Project. When you create a new Project, it will automatically start at version 1.0. [More on Versions...](/platform/versioning/versions)

### Releases

Creating a Release marks a version as ready to publish and takes a snapshot of the most recent edit of a version. When publishing documentation, all released versions will be included in your documetation under a dropdown selector. [More on Releases...](/platform/versioning/releases)

### Product/API Release Cycle

The simpliest and most common approach is to mirror your product or APIs release cycle. The basic rule of thumb is when you release a new version of your API, you release the same version in Stoplight. This release flow is one-to-one with your API, and will usually result in a large number of released versions within Stoplight.

### Platform Versions

If you are creating a documentation driven project, you can describe one or two major versions of your platform via versioning. Then re-release the same versions as you continue your work and display the newest updates in your published documentation.

## Icons and Tooltips

- Solid Upload: A released Version
- Outlined Upload: A Version that has not yet been released
- Code: A sorted folder of versions of the same MAJOR

---

**Related Articles**

- [Versions](/platform/versioning/versions)
- [Releases](/platform/versioning/releases)
- [Read, Design, & Code View](/platform/editor-basics/read-design-code-view)
- [Working with Files](/platform/editor-basics/working-with-files)
- [Import Files](/platform/editor-basics/import-files)
- [Export Files](/platform/editor-basics/export-files)
- [Change History](/platform/editor-basics/change-history)
- [Editor Configuration](/platform/editor-basics/editor-configuration)
- [Environments](/platform/editor-basics/environments)
- [File Validation](/platform/editor-basics/file-validation)
