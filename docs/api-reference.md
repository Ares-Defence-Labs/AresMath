# Complete public API reference

Import `package:ares_math/ares_math.dart`.

## AresMath

| Member | Contract |
| --- | --- |
| `static Future<AresMathLicenceStatus> configure({String? licenceKey, Future<void> Function()? prepareHandwritingRuntime})` | Installs/replaces the process-wide Math key. A null argument uses the `ARES_MATH_LICENCE_KEY` build define. Invalid/missing keys leave trial access. Does not reset the trial. |
| `static String solve(String equation)` | Synchronously returns native solution/working text. No camera/model setup required. May throw AresMathLicenceException or ArgumentError. |
| `static Future<AresMathScanResult?> scan(BuildContext context, {String? licenceKey, String? initialImagePath, String? initialEquation, int countdownSeconds = 3})` | Uses an explicit key when supplied, otherwise preserves existing configuration (or initializes the build-defined key), then presents the supplied scanner route. Countdown accepts 1–10. Cancellation/unmounted context returns null. |

Advanced hosts that already deliver ONNX as an on-demand native feature can supply `prepareHandwritingRuntime`. The SDK awaits it before creating handwriting inference sessions. It prepares dependencies and cannot override native licence checks. Omission preserves the previously configured callback; default standalone integrations need no callback. Hosts that exclude the bundled runtime must supply a compatible runtime before inference.

## AresMathLicenceStatus

Immutable configuration snapshot, with `bool licensed`, `Duration trialRemaining`, and `bool allowed`. `allowed` is true for a valid licence or positive trial time. This is a snapshot for UI; native operations always recheck authorization. Its const constructor accepts required `licensed` and `trialRemaining`.

## AresMathScannerScreen

A StatefulWidget with a const constructor accepting `Key? key`, `String? initialImagePath`, `String? initialEquation` and `int countdownSeconds = 3`. Configure the SDK before mounting it directly. It owns the camera UI; it is not a camera-only controller API. The supported camera integration in this release is the supplied scanner screen.

## AresMathScanResult

An immutable result constructed with required `String equation`, required `String solution`, required `AresMathDisplayMode displayMode` and optional `String? sourceImagePath`. It describes the recognised/corrected equation, display-text solution, chosen mode and optional source photograph path. Temporary image files remain the caller's responsibility if they need to be retained.

## AresMathDisplayMode

Enum values `liveOverlay` and `digitalResult`.

## AresMathLicenceException

Const Exception with no arguments. Thrown by the native text-solving adapter when the evaluation trial has expired and no current Math entitlement is installed. Its message is suitable for diagnostics; use the type for control flow.

## AresMathModels

| Member | Contract |
| --- | --- |
| `static const String packId` | `ink_math_handwriting` |
| `static const int downloadSizeBytes` | `7593285` bytes of model/vocabulary/licence payload, before store compression. |
| `static Future<void> download({void Function(String message)? onProgress})` | Activates the whole store-managed pack, reports progress text and verifies file sizes/SHA-256. Reuses valid cached files. |
| `static Future<void> remove()` | Serializes removal, closes active handwriting sessions and releases/evicts store assets. |
| `static Future<void> cancelDownload()` | Requests native store cancellation. |
| `static Future<AresMathModelStatus> status()` | Returns the current native store state for the pack. |

## AresMathModelStatus

Immutable fields: `String status`, `int downloadedBytes`, `int totalBytes`, `double progress`, and computed `bool installed`. `status` follows the store SDK states: unknown, notInstalled, pending, downloading, transferring, waitingForWifi, requiresUserConfirmation, installed, failed or cancelled as supplied by the native implementation. `progress` is 0–1; totals can be zero when the store has not provided them. Its const constructor requires all four stored fields.

`lib/src` types, channels, native helper classes, filenames and test keys are internal implementation details. They are not additional supported public APIs. Compatibility aliases retained for owner migration are not the recommended customer surface.
