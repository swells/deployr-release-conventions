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

  `v7.3.5-beta.0`

  `v7.3.5-beta.2`

  `v7.3.5-beta.3`

### Prerelease Identifiers

An additional (optional) identifier string that will append the value of the version string as a prerelease identifier.

Example:

  `v7.3.5-beta.0`

## Tag

```bash

$ 

```





