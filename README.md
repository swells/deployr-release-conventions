DeployR Release Conventions
===========================

The goal of this document is to layout _git_ conventions that will aid DeployR releases in order to inform the public of what changes have been made in each version. This is necessary at the development and release stage such that the user can make a decision about when to upgrade. 

- [Release steps](#user-content-release-steps)
  - [Semantic Versioning](#user-content-semantic-versioning)
  - [Tagging](#user-content-tagging)
  - [Marking _release_](#user-content-marking_release)
  - Generating CHANGELOG.md
    - Recognizing unimportant commits
    - Provide more information when browsing the history
  - [Repository wiki](#user-repository-wiki)
    - [Template](#user-template)
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

A possible prerelease identifier for _v7.3.5_ could be: 

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

Once the master branch has been [tagged](#tagging) with the appropriate [release points](#semantic-versioning), we can begin to prepare that tag for a release. Marking the tagged historical version as a _release_ is done from Github using their [Releases](https://github.com/blog/1547-release-your-software) workflow.

In Github:

1. Click the _releases_ link at the top of the repository.
2. Click the _Create a new release_ button.
3. Choose the _Tag version_ from the drop-down list (or input field if this is the first release).
4. Give the release a title based on the [semantic version](#semantic-versioning). _Release titles_ should adhere to the [release title conventions](#release-title-convention).
5. Add release notes. _Release notes_ should adhere to the [release notes conventions](#release-notes-convention).
6. If appropriate, attached the release _binaries_ by dragging and dropping them to the page or via the file chooser.
7. Finally, publish the tagged release by clicking the _Publish release_ button.

### Release Title Convention

The title of a release should only contain its corresponding [semantic version](Semantic Versioning) minus the **v** from the version string. In addition, if the semantic version contains a [prerelease identifier](#prerelease-identifiers) replace the delimited **-** character with a space.

For example, the _release title_ for version:

- _v7.3.3_  ----> `7.3.3`
- _v7.3.3-beta-1_  ----> `7.3.3 beta 1`

### Release Notes Convention

Release notes should be brief and contain the following:

1. A _Release Announcement_ link. This link will point to the offical marketing announcement.
2. A _Change History Rollup_ link. See the [change log](#change-log) section for more information on how to create it.
3. A note on how to get a hold of the release via git:
  `Github: git checkout v7.3.3-beta-1`
4. The attached binary zip of the release build (download this for local deployments)

## Repository wiki

Each repository should have a wiki that follows the [template](#template) below. The official user guides and API documents are hosted on [deployr.revolutionanalytics.com](http://deployr.revolutionanalytics.com) when appropriate. The repository's wiki is where you can maintain a living document that are relevant to the people who are interested in contributing code or feedback.

### Template

```
# Welcome to the {YOUR_REPOSITORY} development wiki!

{YOUR_REPOSITORY}'s official user guides and API docs are hosted on 
http://deployr.revolutionanalytics.com. This wiki is where we maintain 
a living document that is relevant to the people who are interested in 
contributing code or feedback.

# Current Release

## {YOUR_REPOSITORY} {SEMANTIC_VERSION}

- Link --> GitHub release notes page
- Link --> {YOUR_REPOSITORY} {SEMANTIC_VERSION} Change History Rollup
- Link --> Zip dist file
- Link --> Maven Central repository 'ArtifactId' (when appropriate)
- Link --> npm module (when appropriate)

## Past Releases

- Link --> {YOUR_REPOSITORY} {SEMANTIC_VERSION} Change History Rollup
- Link --> {YOUR_REPOSITORY} {SEMANTIC_VERSION} Change History Rollup
- Link --> {YOUR_REPOSITORY} {SEMANTIC_VERSION} Change History Rollup
...

# Future

TDB

# Development

- Link --> Deprecation Policy (TBD)
- Link --> Contribution Standards (TBD)

```




