# Android Signing Identity — Release Repository Requirement

This policy applies to every Android APK built from `wal-studio/WAL-Official-Releases`, including internal test builds, release candidates, and official releases.

## Immutable identity

- Application ID: `com.wayward.launcher.official.wal`
- Required official signing certificate SHA-1: `D9BE7443EB247D27C958CC4250D7F5D1E078F740`

## Mandatory behavior

1. Sign every APK from this repository with the existing official key matching the required SHA-1.
2. Never use a debug, temporary, generated, or alternate key as a fallback.
3. If the official key or its protected credentials are unavailable, fail the signing/build step. Do not produce a substitute-signed APK.
4. Inspect the certificate embedded in the actual output APK and compare its SHA-1 with the required value. Build configuration or a keystore filename is not sufficient evidence.
5. Treat a missing or mismatched certificate as a hard failure. Do not distribute the APK or use it for installation, update, OAuth, or CloudSave compatibility testing.
6. Keep the keystore, private key, and passwords out of Git. Use protected CI secrets or another explicitly approved secure signing mechanism.
7. Preserve the application ID and signing identity to maintain Android update continuity and integrations such as Google OAuth and CloudSave.

## Scope

This requirement is specific to Android artifacts produced from the official release repository. It does not require experimental APKs from the separate Android development repository to use the production signing key.

The README states the policy; build automation must independently enforce it by inspecting the actual APK certificate and failing on mismatch. A documentation-only check is not proof that the build pipeline enforces the requirement.
