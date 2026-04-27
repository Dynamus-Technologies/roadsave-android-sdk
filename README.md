# RoadSave SDK — Android

> **Crash detection. Trip detection. Activity recognition.**
> An Android library (AAR) for RoadSave-powered Android applications, supporting both
> Google Mobile Services (GMS) and Huawei Mobile Services (HMS) devices from a single artifact.

---

## Requirements

| Requirement | Minimum |
|---|---|
| Android API | 24 (Android 7.0 Nougat) |
| compileSdk / targetSdk | 35 |
| Kotlin | 2.0 |
| Gradle | 8.5 |
| Android Gradle Plugin | 8.5 |
| JDK | 11 |

## Installation

> **Phase 1 (current):** manual AAR drop.
> A Maven coordinate (`com.roadsave.lib:roadsave-sdk:<version>`) will replace this in the next
> release line.

### 1. Download

From the [Releases](../../releases) page, download:

- `roadsave-sdk-4.0.0.aar`
- `roadsave-sdk-4.0.0.aar.sha256`

Verify the checksum:

```sh
shasum -a 256 -c roadsave-sdk-4.0.0.aar.sha256
```

### 2. Drop the AAR into your app

Place `roadsave-sdk-4.0.0.aar` in your app module's `libs/` directory (create it if needed).

### 3. Declare the AAR + runtime dependencies

The AAR bundles the GMS/HMS abstraction layer, but the GMS and HMS service libraries themselves
must be declared by your app:

```gradle
repositories {
    google()
    mavenCentral()
    maven { url 'https://developer.huawei.com/repo/' }
}

dependencies {
    implementation files('libs/roadsave-sdk-4.0.0.aar')

    // Networking
    implementation 'com.squareup.okhttp3:okhttp:4.12.0'

    // Coroutines
    implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:1.9.0'

    // AndroidX
    implementation 'androidx.appcompat:appcompat:1.7.0'
    implementation 'androidx.localbroadcastmanager:localbroadcastmanager:1.1.0'

    // Google Mobile Services (required on devices with Google Play Services)
    implementation 'com.google.android.gms:play-services-location:21.1.0'
    implementation 'com.google.android.gms:play-services-base:18.5.0'
    implementation 'com.google.android.gms:play-services-basement:18.4.0'

    // Huawei Mobile Services (required on Huawei devices without GMS)
    implementation 'com.huawei.agconnect:agconnect-core:1.9.5.300'
    implementation 'com.huawei.hms:base:6.5.0.300'
    implementation 'com.huawei.hms:maps:5.3.0.300'
    implementation 'com.huawei.hms:location:6.4.0.300'
}
```

For full integration steps (manifest entries, permissions, runtime initialisation):

**[docs.roadsave.co.za/android/integration-guide/](https://docs.roadsave.co.za/android/integration-guide/)**

## Documentation

Full documentation, integration guide, and API reference:

**[docs.roadsave.co.za/android/](https://docs.roadsave.co.za/android/)**

## License

Proprietary — © CrashDetech (Pty) Ltd t/a RoadSave. All rights reserved.
See [LICENSE](LICENSE) for terms.
