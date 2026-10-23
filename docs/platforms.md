# Platforms and permissions

| Requirement | Version |
| --- | --- |
| Flutter | 3.44+ |
| Dart | 3.12.2+ |
| Android | API 24+; compile SDK 36 |
| iOS | 16.0+ |

The supported targets are Android and iOS. AresMath's text API is part of the native Flutter plugin on those platforms. A command-line Dart package or desktop/web production solver is not included in this release.

## Android

The library declares camera access and bundles its Latin printed-text recognizer for first-use offline capture. The scanner requests runtime camera permission before starting its native preview; the host app can also explain/request that permission in its own onboarding. Image selection uses image_picker and the platform photo picker. Text-only calls do not require camera permission. Configure Google Play model delivery if using handwriting.

The native SDK includes the inference runtime. No Edge package, Edge licence, Live Text plugin, :opencv_stripped module or AresScan project is required. Standard dependency resolution downloads public build dependencies at development/build time; that is separate from on-device equation processing.

## iOS

Set the application's minimum target and Podfile platform to iOS 16.0. Add NSCameraUsageDescription and NSPhotoLibraryUsageDescription to Info.plist with accurate user-facing reasons. The source/customer plugin uses static native framework linkage with ONNX Runtime dependencies. Keep the SDK's required native linker flags; they retain the synchronous solver entry point.

Flutter may use CocoaPods compatibility for plugins whose dependencies do not yet support Swift Package Manager. Do not replace a host application's existing dependency configuration blindly. Follow the example and its matching platform settings.

Vision OCR runs locally. Configure Apple resources for handwriting model delivery. Device signing and store capability/resource configuration belong to the host application.

## Android apps with other native SDKs

Math bundles the shared C++ runtime required by its native engine. If another SDK
(such as C2PA) also supplies `libc++_shared.so`, Gradle can report duplicate JNI
files during `mergeDebugNativeLibs` or `mergeReleaseNativeLibs`. Configure the
host application's `android/app/build.gradle.kts` to package one runtime per ABI:

```kotlin
android {
    packaging {
        jniLibs {
            pickFirsts += "**/libc++_shared.so"
        }
    }
}
```

Keep one compatible runtime in the base app; do not exclude every copy. In the
AresScan+ integration, both runtime candidates were checked against the C++
symbols required by Math and C2PA across arm64-v8a, armeabi-v7a, x86_64 and x86.
Repeat native compatibility and page-alignment checks when upgrading those
dependencies. Android documents [JNI packaging](https://developer.android.com/reference/tools/gradle-api/9.0/com/android/build/api/dsl/JniLibsPackaging)
and [shared C++ runtime requirements](https://developer.android.com/ndk/guides/cpp-support).
