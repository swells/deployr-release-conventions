Deployr Release Conventions
===========================

The goal of this document is to layout _git_ convestions that will aid DeployR releases in order to inform the public of what changes have been made in each version. This is nessary at the development and release stage such that the user can make a decision about when to upgrade. 

- [Release steps](#user-content-release-steps)
  - [Semantic Versioning](#user-content-semantic-versioning)
  - [Tagging](#user-content-tagging)
  - [Marking _release_](#user-content-marking_release)
  - Generating CHANGELOG.md
    - Recognizing unimportant commits
    - Provide more information when browsing the history
  - Repository notes
    - WIKI
    - History
    - Changelog rollup
- Format of the commit message
  - Subject line
  - Allowed <type>
  - Allowed <scope>
  - Message body
  - Message footer
  - Breaking changes
  - Referencing issues
- Examples

# Release steps

## Semantic Versioning

For the official Semantic Version documentation head to [semver.org](http://semver.org/). This is a breif introduction and does not cover all parts of semantic versioning.

### Format

A Semantic Version will be in the format {major}.{minor}.{patch}-{tag}

Example:
 
  `v7.3.5`

  `v7.3.5-beta-0`

  `v7.3.5-beta-2`

  `v7.3.5-beta-3`

#### Prerelease Identifiers

An additional (optional) string will be append to the value of the version string as a prerelease identifier.

A possbile prerelease identifier for _v7.3.5_ could be: 

  `v7.3.5-alpha-0`
  
  `v7.3.5-beta-2`

  `v7.3.5-rc-1`

## Tagging

When the state of the release branch is ready to become a real release, some actions need to be carried out. 

- The release branch is merged into master (since every commit on master is a new release by definition). 
- The commit on master must be tagged for easy future reference to this historical version. 

To _tag_ master:

1. Use tags to mark commits with version numbers:

   ```
   $ git tag -a v7.3.0 -m 'Version 7.3.0'
   ```

2. We have to then _push tags upstream_ because this is not done by default:

   ```
   $ git push --tags
   ```

This produces a version string of the allowing format: 

```
v7.3.0-0-123456789123456789dsdfsfsf
^      ^  ^
|      |  |
|      |  SHA of HEAD
|      |
|      number of commits since last tag
|
last tag
```

## Marking Release

Once the master branch has been [tagged](#tagging) with the appropriate [release points](#semantic-versioning), we can begin to prepair that tag for a release. Marking the tagged historical version as a _release_ is done from Github using their [Releases](https://github.com/blog/1547-release-your-software) workflow.

In Github:

1. Click the _releases_ link at the top of the repository
2. Click the _Create a new release_ button
3. Choose the _Tag version_ from the drop-down list (or input feild if this is the first release)
4. Give the release a title. _Release titles_ should adhear to the [release title conventions](#title-conventions)
5. Add release notes. _Release notes_ should adhear to the [release notes conventions](#notes-conventions)


