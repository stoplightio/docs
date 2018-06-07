# Versioning and Release

You can declare Versions and Releases within Stoplight to manage and track changes made to your Project over time. You can identify which version/release you are viewing in the top right of the editor. Versions will be marked with a **Branch** icon, while releases will be marked with a **Tag** icon. Stoplight follows the [Semantic Versioning](https://semver.org/) numbering conventions of MAJOR.MINOR.PATCH

- Major Version: When incompatible API changes have been made
- Minor Version: When backwards-compatible functionality have been added
- Patch Version: When backwards-compatible bugs fixes have been added

### Versions

Versions are editable snapshots of your current Project. When you create a new Project, it will automatically start at version 1.0. [More on Versions...](./versions.md)

### Releases

If you want to take a permanent time stamped snapshot of a version, you can create a Release. Once a Release is created, it can be viewed but is no longer editable. [More on Releases...](./releases.md)

## Best Practices

Depending on the focus of your project, we recommend following different versioning patterns for the best work flow experience within Stoplight. For example, if you project's primary focus is documentation you may want to use a different approach than if the focus was modeling out an API, but feel free to use whatever pattern you feel works best for your team!

### Product/API Release Cycle

The simpliest and most common approach is to mirror your APIs release cycle. Everytime you release your API, you release your Project. Likewise, you should create a new version of your project when you are ready to start working on new or "breaking" changes to your API. This workflow is more sequential and will lead to a large amount of versions and releases.

### Different Workspaces

Sometimes a project may not follow a typical product release cycle. For example, you may have a project where you want to manage multiple workspaces. For this case, we suggest creating one version for each major workspace, in the start, and then many releases to track the growth and progress of each. When using this approach, it is important to note that you will not be able to move work back and forth between each version, unless you copy it over manually. The benefit being that it allows your team to manage different versions of a project at the same time and then document them under the same domain when publishing.

## Icons and Tooltips

- Pencils: Most up to date work in that Version that has not been Released
- Latest: Most recent version in your project, this is where you will primarily be working
- Star: Highest Release (only one)
- Tag: Released (not editable)

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
