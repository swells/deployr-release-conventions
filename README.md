Deployr Release Conventions
===========================

The goal of this document is to layout _git_ convestions that will aid DeployR releases in order to inform the public of what changes have been made in each version. This is nessary so that the user can make a decision about when to upgrade. 

- [Release steps](#user-content-release-steps)
  - [Semantic Versioning](#user-content-semantic-versioning)
  - [Tagging _master_](#user-content-tag)
  - Marking tag as _current release_
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

For the official Semantic Version docs head to [semver.org](http://semver.org/).

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

## Tag

1. Use tags to mark commits with version numbers:

   ```
   $ git tag -a v7.3.0 -m 'Version 7.3.0'
   ```

2. We have to then _push tags upstream_ because this is not done by default:

   ```
   $ git push --tags
   ```

You can then we use the describe command:

```
$ git describe --tags --long
```

This produces a version string of the allowing format:

```
v7.3.0-0-123456789123456789dsdfsfsf
^      ^  ^
|       |   |
|       |   SHA of HEAD
|       |
|       number of commits since last tag
|
last tag
```







