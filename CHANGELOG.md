# Release Notes — RoadSave Android SDK

Public-facing release notes for the RoadSave Android SDK. Versioned per
[Semantic Versioning](https://semver.org/) starting from `4.0.0`. Breaking changes are
prefixed `BREAKING:`.

For installation instructions see
[docs.roadsave.co.za/android/](https://docs.roadsave.co.za/android/).

---

## [Unreleased]

(no public-facing changes pending)

---

## [4.0.0-rc.1] — 2026-04-27

First public pre-release of the RoadSave Android SDK 4.0.0. API is frozen; this release
is intended for integration testing by early adopters before the `4.0.0` stable cut.

### Added

- Public distribution via `Dynamus-Technologies/roadsave-android-sdk` — single AAR covering
  both Google Mobile Services (GMS) and Huawei Mobile Services (HMS) devices.
- SHA-256 verified download from the GitHub Releases page.
- `docs.roadsave.co.za/android/` documentation site with integration guide, API reference,
  downloads page, and changelog.

### Notes

- Install instructions: [docs.roadsave.co.za/android/downloads/](https://docs.roadsave.co.za/android/downloads/)
- Phase 2 will introduce a Maven coordinate (`com.roadsave.lib:roadsave-sdk:4.0.0`) to
  replace the manual AAR drop.

---

## [4.0.0] — 2026-04-23

First public release of the RoadSave Android SDK under the `com.roadsave.lib` package namespace.
Supports both Google Mobile Services (GMS) and Huawei Mobile Services (HMS) devices from a
single AAR.

### Added

- `RoadSave` — primary SDK entry point replacing `CrashDetech`.
- `RoadSaveConfiguration` — SDK configuration builder replacing `CrashDetechConfiguration`.
- `RoadSaveListener` — callback interface replacing `SdkEventListener`. Delivers trip events,
  crash events, activity-recognition state, and error codes.
- `RoadSaveBroadcastConstants` — broadcast action and extras constants replacing
  `CrashDetechBroadcastConstants`.
- `RoadSaveLocation` — location data type replacing `CrashDetechLocation`.
- `CrashInfo`, `CrashConfidence`, `CrashFalsePositiveReason` — crash event types replacing
  their `CrashDetech*` predecessors.
- `CurrentTripInfo`, `TripInfo`, `TripStartInfo` — trip event types replacing their
  `CrashDetech*` predecessors.
- `ErrorCode` — unified error enum replacing the individual `CrashDetech*Error` constants.
- `RoadSave.setAutoTripDetection(Boolean)` — runtime toggle to pause and resume automatic
  trip detection without reinitialising the SDK.
- Mock provider API (`RoadSave.setMockLocationProvider()` / `setMockSensorProvider()`,
  debug builds only) for integration testing with scripted GPS and accelerometer data.
- OkHttp HTTP client for crash evaluation requests.
- `consumer-rules.pro` ProGuard/R8 keep rules shipped inside the AAR; no manual R8 config
  required by consuming apps.
- Kotlin public API throughout; all public types have KDoc.
- Dokka-generated HTML API reference published at
  [docs.roadsave.co.za/android/api/](https://docs.roadsave.co.za/android/api/).
- Minimum Android API level: **24** (Android 7.0 Nougat).

### Changed

- BREAKING: Package root changed from `com.crashdetech.lib` to `com.roadsave.lib`. Update
  all import statements.
- BREAKING: Broadcast action strings changed from `com.crashdetech.lib.*` to
  `com.roadsave.lib.*`. Update any `BroadcastReceiver` action comparisons and
  `<intent-filter>` entries in `AndroidManifest.xml`.
- BREAKING: AAR artifact renamed from `crashdetechlibrarysdk-<version>.aar` to
  `roadsave-sdk-<version>.aar`. Update your `libs/` path and `build.gradle` reference.
- Minimum Android API level raised from 21 to **24**.
- `RoadSaveConfiguration.shouldAutoDetectTrips` now correctly controls whether automatic
  trip detection starts at SDK initialisation; previously the flag was a no-op at init time.

### Removed

- BREAKING: All `CrashDetech*` public types removed. See the migration table in the
  [integration guide](https://docs.roadsave.co.za/android/integration-guide/) for the full
  before/after mapping.

### Migrating from 3.x

See the full migration guide at
[docs.roadsave.co.za/android/integration-guide/](https://docs.roadsave.co.za/android/integration-guide/).

Quick-reference type rename table:

| 3.x | 4.0.0 |
|---|---|
| `CrashDetech` | `RoadSave` |
| `CrashDetechConfiguration` | `RoadSaveConfiguration` |
| `CrashDetechBroadcastConstants` | `RoadSaveBroadcastConstants` |
| `CrashDetechLocation` | `RoadSaveLocation` |
| `SdkEventListener` | `RoadSaveListener` |
| `CrashDetechCrashInfo` | `CrashInfo` |
| `CrashDetechCrashConfidence` | `CrashConfidence` |
| `CrashDetechCrashConfidenceHIGH/LOW/UNKNOWN` | `CrashConfidence.HIGH/LOW/UNKNOWN` |
| `CrashDetechCrashFalsePositiveReason` | `CrashFalsePositiveReason` |
| `CrashDetechCurrentTripInfo` | `CurrentTripInfo` |
| `CrashDetechTripInfo` | `TripInfo` |
| `CrashDetechTripStartInfo` | `TripStartInfo` |
| `CrashDetechErrorCode` | `ErrorCode` |
| `CrashDetechAccelerometerError` | `ErrorCode.AccelerometerError` |
| `CrashDetechConfigError*` | `ErrorCode.ConfigError*` |
| `CrashSDKStopped` | `ErrorCode.SdkStopped` |
