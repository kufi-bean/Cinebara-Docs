# Assets

An asset is anything that can be tracked by an asset server and served to Cinebara. These are commonly referenced by nodes and serve a high range of roles.

## Asset Server

The asset server is responsible for serving assets (no way!).
Assets are associate to both a path and an Id. References to assets should be held by Id, but an asset may also be queried by path.
Assets are stored in a single flat folder and its name is its ID within the database. Metadata for the asset is stored in JSON as another column in the DB.
If the same asset is stored twice, it is not saved as a separate file, rather, the asset points back to the already existing resource.

Loading an asset into a session does not mean it sits on an asset server. Rather, it is in session storage until something is explicitely saved that uses the asset. This can be thought of as an overlay of the asset server, you resolve what is in the session assets before the actual asset server.

!!!question What happens if the session closes unexpectedly?
Should sessions auto-save periodically, causing edited assets to gain new versions?
Or should edited assets keep a locally saved version on disk which would survive shutdown?
!!!

## Asset Repositories

When you open the asset drawer you are presented with your local repository. The local repository stores your personal assets and does not belong to any server. Only the local user can access this repository.

Repositories are distinct scopes for assets to live in. Assets may have contents which refer to other assets within the same repository. Assets may not reference assets outside of their repository.

## Referencing assets from another repo

To use assets that belong to another repository, a linked asset is used. A linked asset is a local copy of an asset from another repo with a bit of metadata about where it was originally loaded from. Linked assets cannot be modified. However, you may unlink the asset to make it an owned copy which is free for mutation. Unlinking will preserve links for referenced assets contained within the unlinked asset, so a recursive unlink is also provided to make a completely local copy.

## Dependencies

A repository may depend on other repositories, quite like github submodules. The entire referenced repository should probably be copied to ensure that each repo can stand on its own, but that may be optional.

## Version control

Creating a commit in a repository takes a snapshot of the state of the repo, or at least the changes since the last snapshot. These commits are uniquely identifyable and a commit must be referenced by repos that intend to use dependencies.

Some assets may support even more granular version control. A Stage, for example, records every change that is made to it and each time it is saved, a new artifact is made for the stage asset that preserves these "diffs".

Modifying and saving an asset creates another artifact for it. This could be problematic for large assets being modified, so we may want to consider "live artifacts" allowing for drop-in replacements of artifacts and reducing duplication. To be discussed.

=== Open Questions
- Can you commit versions of assets without committing the entire project?
- When modifying an asset and saving, does it automatically save a new artifact or replace the existing one?
- Are repos replicated locally when hosting one from a server?
- How does hosting a repo on a server work in comparison to hosting one locally for a session?
- Can multiple sessions be open for the same repo at once?
- How do linked assets work? Do you link entire projects as "sub-projects"?
- Do we have dependencies? A project could depend on another project from another repo / asset server. This could be how asset linking works.
- Does saving an asset always make a new artifact or does that require an explicit commit?
- How do permissions / ownership work?
- Who can use your repo as a dependency? Is it a public / private system or more flexible?
==-

## Implementation steps

- [x] Creating a repo
- [ ] Opening an existing repo
- [ ] Hosting a repo in a session
- [ ] Hosting a repo persistently
- [ ] Using a persistent repo in a session
- [ ] Making commits in a repo
- [ ] Restoring to previous commits
- [ ] Repo branches
