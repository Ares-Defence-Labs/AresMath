# Model delivery and lifecycle

The native inference runtime is bundled with the standalone SDK. Handwriting recognition uses the optional `ink_math_handwriting` pack, delivered through Google Play Asset Delivery, Apple Managed Background Assets on newer iOS, or Apple's ODR fallback. No direct GitHub/model HTTP downloader is included in the SDK.

The package supplies the public CoMER weights, vocabulary, licence and platform pack definitions under `distribution/`. The host application must include/upload the corresponding pack in its own store release. A pub.dev dependency cannot create store-hosted resources for another app automatically.

| File inside pack | Bytes |
| --- | --- |
| `models/encoder_int8.onnx` | 3460779 |
| `models/decoder_int8.onnx` | 4118047 |
| `models/vocab.json` | 3697 |
| `models/LICENSE.comer.txt` | 10762 |

All four files are resolved from one installed pack and checked against pinned SHA-256 values before use. Keep the licence file with the model. These third-party open model assets are separate from the proprietary compiled Math engine.

## Android

Copy `distribution/android/ink_math_handwriting` into your app's `android/asset_packs/ink_math_handwriting` directory. In settings.gradle.kts, declare the asset-pack plugin at the same Android Gradle Plugin version as the app, then register the project:

```kotlin
include(":ink_math_handwriting")
project(":ink_math_handwriting").projectDir = file("asset_packs/ink_math_handwriting")
```

In the app module's android block:

```kotlin
assetPacks += listOf(":ink_math_handwriting")
```

Build an Android App Bundle and upload through your normal Google Play release process. Use bundletool local testing or an internal Play release for actual on-demand delivery. A directly installed debug APK does not provide Google Play-hosted model resources. Printed Latin OCR is bundled with the native SDK; it does not require a separate Play-services recognition-module download. Do not globally substitute that dependency with an unbundled recognizer unless your host deliberately provisions the replacement module.

## Apple

Copy `distribution/apple/ink_math_handwriting/models` into your host application's resources. Register each file as a resource with the `ink_math_handwriting` on-demand resource tag. Enable on-demand resources. Keep `LICENSE.comer.txt` as named; a generic LICENSE resource can conflict with other packs. The supplied manifest records relative paths and checksums.

For iOS 26+ Managed Background Assets, include the corresponding model pack in the host application's managed asset archive/catalogue and Background Download extension using its existing asset-store manager setup. ODR is the fallback where applicable. Host app signing, App Store upload and resource hosting remain host release tasks.

## Manage the model

```dart
await AresMathModels.download(onProgress: (message) => showStatus(message));
final status = await AresMathModels.status();
await AresMathModels.cancelDownload();
await AresMathModels.remove();
```

The scanner activates the same pack automatically when handwriting inference is needed. The text API does not use this pack. Removal waits for native inference sessions to close before eviction. Re-download activates/validates the store-managed files again. Do not delete files manually while sessions are using them. OS store eviction can make a later activation/download necessary.

If verification fails, remove and re-download the pack. If it is unavailable, check your app's pack registration/store release rather than substituting an arbitrary URL. Actual store-hosted delivery must be validated against the host application's uploaded release; local packaging and lifecycle tests do not establish that roundtrip.

## Hosts with an existing on-demand runtime

The default customer SDK bundles ONNX. An owner host that deliberately excludes that native dependency can pass prepareHandwritingRuntime to AresMath.configure and activate its existing shared native feature there. The callback is awaited before session creation, while Math model files continue to use their own pack. It cannot grant a licence or replace model checksum verification.
