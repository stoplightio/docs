# Releases

## What

Creating a Release marks a version as ready to publish and takes a time stamped snapshot of a the most recent edit of a version. When publishing all released versions will be included in your documetation under a dropdown selector. These are useful for pointing to specific points of your project and allowing you to continue editing a version without altering published documentation.

## How

1.  Select the **Project** you wish to modify
2.  In the top right, select the **Branch** icon with the version
    number

### Create a New Release

1.  While editing a version, click **Release x.x.x**

    - Optional: Add Release Notes

> If you only have read access to a project , the section will instead display your previous release notes if any were entered.

### Delete a Release

1.  While editing a version, click the **Trash Icon** under the Edit a Release section

### Edit a Release

1.  While editing a version, click **Rerelease** under the Edit a Release section

    - Optional: Add/Change Release Notes

> Rereleasing a version will update the git tag to point to the newest most recent commit/changes to your version.

## Notes

Git tags are used internally to manage releases. Under the hood for each release, a tag is created as `release/{VERSION}` and is a reference to the most recent commit in the version branch `version/{MAJOR.MINOR}`.

It is important to note that a change in a released version will need to be re-released and re-published if you want those changes to be reflected in your published documentation.

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
