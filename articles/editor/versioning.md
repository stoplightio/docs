# Versioning and Release 

## What 
You can declare Versions and Releases within Stoplight to manage changes made to your Project over time.  Stoplight follows the [Semantic Versioning](https://semver.org/) numbering conventions of MAJOR.MINOR.PATCH
- Major Version: When incompatible API changes have been made 
- Minor Version: When backwards-compatible functionality have been added 
- Patch Version: When backwards-compatible bugs fixes have been added

### Versions
Versions are editable snapshots of your current Project. When you create a new Project, it will automatically start at version 1.0. 

### Releases 
If you want to take a permanent time stamped snapshot of a version, you can create a Release. Once a Release is created, it can be viewed but is no longer editable. 

## How 
1. Select the **Project** you wish to modify
2. In the top right, select the **Branch** icon with the version number 

### To Create a New Release 
1. Select the Version you would like to Release and click **Release x.x.x**

> Optional: Add Release Notes

### To Create a New Version 
1. Input a new Version Number, then click **+ Version x.x**

> New versions will be generated from the nearest Version numerically lower than it 

## Icons and Tooltips 
- Pencils: Most up to date work in that Version that has not been Released 
- Latest: Highest Release in the highest version that is editable 
- Star: Highest Release (Only one)
- Tag: Released but not editable 

---
**Related Articles**
- [Read, Design, & Code View](/platform/editor-basics/read-design-code-view)
- [Working with Files](/platform/editor-basics/working-with-files)
- [Import Files](/platform/editor-basics/import-files)
- [Export Files](/platform/editor-basics/export-files)
- [Change History](/platform/editor-basics/change-history)
- [Editor Configuration](/platform/editor-basics/editor-configuration)
- [Environments](/platform/editor-basics/environments)
- [File Validation](/platform/editor-basics/file-validation)
