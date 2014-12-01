DeployR Release Conventions
===========================

The goal of this document is to layout _git_ conventions that will aid DeployR releases in order to inform the public of what changes have been made in each version. This is necessary at the development and release stage such that the user can make a decision about when to upgrade. 

- [Release steps](#user-content-release-steps)
  - [Semantic versioning](#user-content-semantic-versioning)
  - [Tagging](#user-content-tagging)
  - [Marking _release_](#user-content-marking-release)
  - [Changelog](#user-content-changelog)
    - [Generating CHANGELOG.md](#user-content-generating-changelogmd)
  - [Repository wiki](#user-content-repository-wiki)
    - [Template](#user-content-template)
- [Format of the commit message](#user-content-format-of-the-commit-message)
  - [Subject line](#user-content-subject-line)
  - [Message body](#user-content-message-body)
  - [Message footer](#user-content-breaking-changes)
    - [Breaking changes](#user-content-breaking-changes)
    - [Referencing issues](#user-content-referencing-issues)
  - [Examples](#user-content-examples)

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

## Changelog

Changelogs are important in order to understand how previous versions are different from the current release. All changelogs will be generated by a script at the end of a release. At the very least, a skeleton changelog will be emitted. Editing a changelog before the actual release is permitted. 

### Generating CHANGELOG.md

The generated `CHANGELOG.md` will contain three sections:

- New features

New features in this release:

```
$ git log <last release> HEAD --grep feat
```

- Bug fixes

```
$ git log <last release> HEAD --grep fix
```

- Breaking changes

```
$ git log <last release> HEAD --grep BREAKING
```

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

# Get Involved (optional)

- Link --> Deprecation Policy (TBD)
- Link --> Contribution Standards (TBD)

```

## Format of the Commit Message

```
{type}({scope}): {subject}
<BLANK LINE>
{body}
<BLANK LINE>
{footer}
```

Any line of the commit message cannot be longer than 90 characters, with the subject line limited to 70 characters. This allows the message to be easier to read on github as well as in various git tools.

### Subject Line
The subject line contains a succinct description of the change to the logic.

The allowed {types} are as follows:

- feat (feature)
- fix (bug fix)
- docs (documentation)
- style (formatting)
- refactor (refactoring)
- test (adding missing tests)
- chore (maintenance)

The {scope} can be anything specifying the location of the commit change e.g. the controller, the client, the logger, ect. 

The {subject} needs to use imperative, present tense: “change”, not “changed” nor “changes”. The first letter should not be capitalized, and there is no dot (.) at the end.

### Message Body
Just like the {subject}, the message {body} needs to be in the present tense, and includes the motivation for the change, as well as a contrast with the previous behaviour.

### Message Footer

This section is where we annotate any breaking changes or closing defects.

#### Breaking Changes

All breaking changes need to be mentioned in the footer with the description of the change, the justification behind the change and any migration notes required. For example:

 > BREAKING CHANGE: The API interface `pipeline()` has been changed to `batch()`.

#### Referencing issues

Closed bugs should be listed on a separate line in the footer prefixed with the `closes` keyword, for example:

`closes #54321`

Or in the case of multiple issues:

`closes #54321, #9876, #12345`

## Examples

- **feat (feature)**
  
  feat($browser): onUrlChange event (popstate/hashchange/polling)
  
  Added new event to $browser:
    - forward popstate event if available
    - forward hashchange event if popstate not available
    - do polling when neither popstate nor hashchange available

  BREAKING CHANGE: $browser.onHashChange, which was removed (use onUrlChange instead)

- **fix (bug fix)**

  fix($compile): couple of unit tests for IE9

  Older IEs serialize html uppercased, but IE9 does not...
  Would be better to expect case insensitive, unfortunately jasmine does
  not allow to user regexps for throw expectations.

  Closes #392
  
  BREAKING CHANGE: foo.bar api, foo.baz should be used instead

- **docs (documentation)**

  docs(guide): updated docs

  Couple of typos fixed:
  - indentation
  - missing brace

- **style (formatting)**

  style(controller): Whitespace cleanup.

- **refactor (refactoring)**
 
  refactor(controller): Broke public function foo() up into samller private functions.

  public function foo() internally calls:
  - bar()
  - baz()

- **test (adding missing tests)**

  test(controller): Added new test spec for authentication and cookies.

  Cookie check:
  - before
  - after
  
- **chore (maintenance)**






