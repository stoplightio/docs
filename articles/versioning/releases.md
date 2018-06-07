# Releases

## What

If you want to take a permanent time stamped snapshot of a version, you can create a Release. Once a Release is created, it can be viewed but is no longer editable. You should create releases when you want to mark your work as completely done. These are good for tracking the history and growth of your project.

> Releases in Stoplight follow the [Semantic Versioning](https://semver.org/) number conventions and are marked by MAJOR.MINOR.PATCH.

## How

1.  Select the **Project** you wish to modify
2.  In the top right, select the **Branch** or **Tag** icon with the version
    number

### Navigate to a Release

1.  The version or release you are currently viewing will be highlighted in blue in the tree
2.  The item marked with the star is the highest released release within your your project
3.  Select any release

> To easily identify which items are releases, we use the tag icon. It is important to note that Releases are not editable. So when viewing a release, you may make changes in the editor, but features like saving and file deletion are disabled.

### Create a New Release

1.  While editing a version, click **Release x.x.x**

    - Optional: Add Release Notes

> If you are currently veiwing a release, the section will instead display your previous release notes if any were entered.

## Notes

Git tags are used internally to manage releases. Under the hood for each release, a tag is created as `{MAJOR.MINOR.PATH}` and is a reference to the most recent commit in the version branch `version/{MAJOR.MINOR}`.

We HIGHILY suggest that you do not change releases in any way, but if you must, this can be done using git. It is important to note that a change in this release will only be refelected in itself and will not propagate to any other versions/releases.

---

**Related Articles**

- [Versioning & Releases](./introduction.md)
- [Versions](./versions.md)
- [Read, Design, & Code View](/platform/editor-basics/read-design-code-view)
- [Working with Files](/platform/editor-basics/working-with-files)
- [Import Files](/platform/editor-basics/import-files)
- [Export Files](/platform/editor-basics/export-files)
- [Change History](/platform/editor-basics/change-history)
- [Editor Configuration](/platform/editor-basics/editor-configuration)
- [Environments](/platform/editor-basics/environments)
- [File Validation](/platform/editor-basics/file-validation)
