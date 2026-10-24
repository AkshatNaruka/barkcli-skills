---
id: release-prep
name: Release Prep
description: Cut a release without surprises
triggers: [release, changelog, version, tag]
---
# Release Prep

1. **Bump once, everywhere.** Version appears in manifests AND
   generated artifacts; grep the old version to find stragglers.
2. **Changelog from history.** Write entries from the actual commit range
   (`git log <last-tag>..HEAD`), grouped fixed/added/changed. Drop internal
   chore noise.
3. **Freeze test state.** CI must be green on the exact commit you tag —
   not "roughly today".
4. **Tag + notes.** Annotated tag with the changelog summary; verify the
   artifact builds from the tag, not from a dirty checkout.
