# Versioning

While developing applications, version numbers serve as a marker for when new features and fixes have been added to an application. For both developers and clients, version numbers create a common language to help with discussion about the application and the work that has been done to it. For example, instead of using potentially confusing terms like “the last release”, “three releases ago”, “the fix we added after the second release”, we can point to specific version numbers like 1.2, 1.4, or 2.1.2. When we want to look at code for a previous release, we simply check out the commit from “master” with the tag of the release version number.

Version numbers will employ the following format:

1.2.3.4 where:

*   1 is the **major release**
*   2 is the **intermediate release**
*   3 is the **minor release**
*   4 is the **revision** number (optional)

**Major Release**: Signifies a “complete” system with whatever features that version was meant to have. Normally any subsequent “major” versions are rewrites, or architecture changes, or major changes to the software that require a client update.

**Intermediate Release**: Signifies a less significant release, but with many bug fixes, features, or other “minor” events. These will usually include interface changes and additions. These will launch at a slower pace than a minor release, usually quarterly, or if there will be a big interface change.

**Minor Release**: Signifies a low significance, more regular release. These tend to coincide with the end of a development sprint. Normally applications should be somewhat compatible in their “intermediate release” tree, so minor versions of the same intermediate release should be architecturally the same.

**Revision Number (optional)**: Generally signifies just bug fixes, small fixes, and are somewhat insignificant in their scope. It could be something as simple as changing the contrast between the foreground and background of the app. These are small additions made after a minor release.

### How to use

Version numbers will be used on release branches, as the name of the branch, and as tags for commits on master.

**Major release**: We will hardly ever be changing the major release number unless we are rewriting the application.

**Intermediate release**: The intermediate release number will change for our intermediate releases which happen every quarter or so, depending on the project.

**Minor release**: The minor release number will change after every sprint.

**Revision number (optional)**: For bug fixes, stylistic changes, typo fixes, and other small stuff between releases, we will update the revision number.

### How version numbers are used in git

Refer to the [git usage guide](git_usage_guide.md) for this.
