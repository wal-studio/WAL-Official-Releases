SOURCE REPOSITORY: wal-studio/WORK-DO-NOT-TOUCH-RELEASES
SOURCE BRANCH: main
SOURCE PATH: README.md
SOURCE BLOB SHA: 29168150df3ab8ad3f03592d02485f57e9e69e1e

----- ORIGINAL CONTENT BEGIN -----
# WAL Launcher — Official Releases

This repository is the official release and release-candidate repository for WAL Launcher across supported platforms, including Android and PC. It is used both to prepare and test the next release and to publish approved official updates. It is not limited to hosting already-published stable binaries.

## Release repository baseline and workflow

- The baseline for release work is the **most advanced validated test implementation after the latest official update**.
- Unless the user explicitly instructs a version upgrade and official release, continue implementation and testing from that most advanced post-release test version. Do not silently reset work to the last public binary or an older commit.
- Identify the most advanced test implementation by actual integrated functionality, preserved behavior, and verification evidence—not by commit date, commit count, branch name, or version label alone.
- Integrate and test new features only after they have been demonstrated in the development repositories. Preserve the last official update's working behavior and compatibility while doing so.
- Release-candidate builds and tests are permitted in this repository. They are not official releases merely because they are built or uploaded as test artifacts.
- Do not create or publish an official version, stable release, public release announcement, or production promotion unless the user explicitly instructs an official version upgrade/release.
- Keep platform-specific packaging and signing requirements separate. The Android identity requirements below apply to every Android APK built from this repository, including release-candidate and test APKs.

## Android APK identity — immutable

| Field | Required value |
|---|---|
| Package ID | `com.wayward.launcher.official.wal` |
| Official signer certificate SHA-1 | `D9BE7443EB247D27C958CC4250D7F5D1E078F740` |

Every Android APK produced from this repository—including internal test builds, release-candidate builds, and official releases—must be signed with the existing official signing key matching the SHA-1 above.

- Never substitute a debug, temporary, newly generated, or different signing key.
- If the existing official key is unavailable, signing must fail. Do not silently fall back to another key.
- Verify the certificate on the actual generated APK; do not rely only on Gradle configuration, keystore filenames, or build logs.
- A certificate mismatch or missing certificate is a hard failure. Do not distribute or use that APK for installation, update, OAuth, or CloudSave compatibility testing.
- Keep the keystore, private key, and passwords out of the repository. Supply them only through protected build secrets or another approved secure signing mechanism.
- Preserve the package ID and signer identity so Android update compatibility and integrations such as Google OAuth and CloudSave remain intact.

## Android stable release contract

- Publish only fully tested, user-approved stable releases.
- Use a tag matching `vMAJOR.MINOR.PATCH`, for example `v1.0.1`.
- Do not mark stable releases as draft or prerelease.
- Attach exactly one installable, signed APK named `WAL-Android-Launcher-MAJOR.MINOR.PATCH.apk`.
- Attach `SHA256SUMS.txt` with a line in the standard format:
  `<64-character SHA-256>  WAL-Android-Launcher-MAJOR.MINOR.PATCH.apk`
- The GitHub Release asset digest and the checksum file must match the APK bytes.
- `versionName` must match the tag without the leading `v`.
- Derive `versionCode` from the Official Gradle build: `1 + (MAJOR - 1) * 1,000,000 + MINOR * 1,000 + PATCH`. This keeps `v1.0.0` at code `1` and guarantees increasing codes for later versions while `MINOR` and `PATCH` remain below `1000`.
- Release notes should describe user-visible changes and known limitations.

The in-app updater reads only published stable releases, ignores draft/prerelease releases, and verifies the SHA-256, package ID, version, and signing certificate before invoking Android's user-approved package installer.

## Do not upload

- Keystores, private keys, passwords, OAuth secrets, pairing credentials, or user data.
- Unverified builds or Android APKs signed with a different certificate.
- Source archives or temporary CI artifacts as official release assets.

----- ORIGINAL CONTENT END -----
