# WAL Android Launcher — Official Releases

This public repository distributes the stable **WAL Android Launcher** APK only. Application source code and private signing material do not belong here.

## Stable release contract

- Publish only fully tested stable releases.
- Use a tag matching `vMAJOR.MINOR.PATCH`, for example `v1.0.1`.
- Do not mark stable releases as draft or prerelease.
- Attach exactly one installable, signed APK named `WAL-Android-Launcher-MAJOR.MINOR.PATCH.apk`.
- Attach `SHA256SUMS.txt` with a line in the standard format:
  `<64-character SHA-256>  WAL-Android-Launcher-MAJOR.MINOR.PATCH.apk`
- The GitHub Release asset digest and the checksum file must match the APK bytes.
- `versionName` must match the tag without the leading `v`.
- Derive `versionCode` from the Official Gradle build: `1 + (MAJOR - 1) * 1,000,000 + MINOR * 1,000 + PATCH`. This keeps `v1.0.0` at code `1` and guarantees increasing codes for later versions while `MINOR` and `PATCH` remain below `1000`.
- Release notes should describe user-visible changes and known limitations.

## Required APK identity

| Field | Required value |
|---|---|
| Package ID | `com.wayward.launcher.official.wal` |
| Initial version | `1.0.0` |
| Initial versionCode | `1` |
| Release signer SHA-1 | `D9BE7443EB247D27C958CC4250D7F5D1E078F740` |

The in-app updater reads only published stable releases, ignores draft/prerelease releases, and verifies the SHA-256, package ID, version, and signing certificate before invoking Android's user-approved package installer.

## Do not upload

- Keystores, private keys, passwords, OAuth secrets, pairing credentials, or user data.
- Development/debug APKs.
- Unverified builds or APKs signed with a different certificate.
- Source archives or temporary CI artifacts.

SOURCE_BRANCH=temp/release-notes-trigger-20261123
SOURCE_PATH=README.md
