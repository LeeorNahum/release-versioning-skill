---
name: "release-versioning"
description: "Manage versioned releases and release artifacts across software, apps, firmware, skills, packages, and downloadable builds. Use when bumping semver, preparing GitHub releases, syncing README badges/version mentions, publishing binaries or archives, attaching release assets, updating package/app metadata, or making sure version constants and docs agree before a release."
metadata:
  author: "Leeor Nahum"
  version: "1.2.2"
---

# Release Versioning

Treat a release as a contract between code, docs, tags, artifacts, and users.

Do not let the repo say one version while the binary, firmware, README, tag, or release notes say another.

## Release Inventory

Before changing versions, identify every version surface:

- Package metadata: `package.json`, `pyproject.toml`, app manifests, extension manifests
- Code constants: `VERSION`, `APP_VERSION`, firmware build flags, generated about dialogs
- Docs: `README.md`, install docs, badges, changelog
- Artifacts: `.zip`, `.exe`, `.bin`, `.uf2`, `.hex`, app bundles, extension packages
- Git: tags, GitHub releases, release notes
- Deployment records: provider dashboard values, release tables, update manifests

Report which surfaces exist before editing.

## Semver

Use [Semantic Versioning](https://semver.org/) unless the repo already documents a different scheme.

- Patch: bug fixes, wording/docs fixes, internal-only packaging fixes
- Minor: new capability, supported platform, workflow, or compatibility addition
- Major: breaking behavior, renamed package/app, changed public protocol, incompatible firmware/device contract

Use `vX.Y.Z` for Git tags unless the repo already has a different tag convention.

Increment immediately when changes are made for a meaningful checkpoint. Do not wait for a commit, push, or user signal once the work is being finalized as the next accepted state. During initial creation, active drafting, fast review loops, or uncommitted edits the same agent owns, keep the draft's version stable until the work is ready to be treated as the next version.

Before incrementing, inspect the last committed or tagged version via git and compare it to the current working state. If a published, installed, handed-off, or user-approved version is newer than git, use that accepted version as the checkpoint. If multiple uncommitted changes have accumulated across passes since the last checkpoint, calibrate one increment to cover all of them honestly rather than incrementing per-pass in isolation. The version must reflect the true scope of all changes since the last accepted version. If git history is unavailable, use the nearest meaningful checkpoint: the last release, install, handoff, or user-approved draft.

## Workflow

1. Inspect current version surfaces and latest Git tag/release.
2. Decide the next version and explain why.
3. Update all source-controlled version surfaces together.
4. Build or package the release artifact from a clean tree.
5. Verify the artifact name, embedded/displayed version, README, and tag all agree.
6. Create or prepare the GitHub release using the repo's existing release-note style when one exists.
7. Attach or generate release assets according to the repo's existing release process.
8. After publishing, verify the latest-release link, badge, or update channel points to the intended version.

## README Version Badges

For public GitHub projects with releases, prefer a README badge that tracks the latest semantic GitHub release instead of hardcoding a version in prose.

Use a latest-release badge when it helps users quickly identify the current release:

```markdown
[![GitHub Release](https://img.shields.io/github/v/release/OWNER/REPO?sort=semver)](https://github.com/OWNER/REPO/releases/latest)
```

After publishing, verify the badge resolves to the new semver tag and the `/releases/latest` link lands on the intended release.

Do not add noisy badges to tiny private repos, internal-only repos, or docs where a badge would distract more than it helps.

## Release Notes

Pattern-match existing releases first. If there is no established style, write concise user-facing notes that explain what changed and any install/update implications.

Do not paste secret values, local machine paths, or internal scratch context.

## Artifact Rules

- Name release assets with product, version, platform, and format when useful.
- Do not attach stale artifacts from earlier builds.
- Rebuild if version metadata changed after packaging.
- Prefer generated build output over hand-edited archives.
- For downloadable GUI/app releases, make the README install/run instructions match the latest artifact.
- For projects users install from GitHub releases, make the README point to the latest release or use a latest-release badge instead of stale direct asset URLs.
- For skills, bump `metadata.version` at the next meaningful checkpoint after behavior changes and keep README behavior aligned without adding noisy version footers.

## Firmware And Device Releases

Firmware is a versioned release artifact, not a special exception.

When firmware or device updates are involved:

- Identify hardware compatibility before releasing
- Keep firmware version constants/build flags synced with the tag
- Attach the exact binary the device/update service should fetch
- Update any release table, manifest, or update metadata that points devices to the artifact
- Do not mix debug and release artifacts
- Do not publish a device-facing update until the rollback or recovery path is understood

Firmware configuration and secrets belong in a firmware config skill. This skill owns the release artifact and version alignment.

## Stop And Ask

Ask before:

- Choosing a major/minor/patch bump when user impact is unclear
- Publishing a GitHub release
- Replacing an existing release asset
- Marking an update as latest for devices or users
- Changing public package names, executable names, extension IDs, firmware hardware compatibility, or update URLs
