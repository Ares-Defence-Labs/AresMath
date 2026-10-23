[![Ares Defence Labs](https://raw.githubusercontent.com/Ares-Defence-Labs/AresMath/main/branding/ares-defence-labs-banner.png)](https://aresdefencelabs.com)

# AresMath

[Official website](https://aresdefencelabs.com/) · [GitHub repository](https://github.com/Ares-Defence-Labs/AresMath) · [Developer documentation](https://aresdefencelabs.com/development-sdks?sdk=math-scanner&view=overview)

> **Commercial SDK — paid licence required for production use.**
> AresMath is proprietary software from Ares Defence Labs. Developers can
> evaluate scanning and text solving using the shared native 60-second process
> trial. Without a valid licence, both deactivate when the trial expires.
>
> Configure the full signed licence key in application source or private build
> configuration. One customer Math licence covers unlimited apps across supported
> platforms. Ship a replacement key before expiry so existing app installations
> retain access.
>
> [Licensing and availability](https://aresdefencelabs.com/development-sdks?sdk=math-scanner&view=overview) · [Read the commercial licence](https://github.com/Ares-Defence-Labs/AresMath/blob/main/LICENSE)

Commercial Flutter equation capture, on-device recognition and text-solving SDK
for Android and iOS. Point the camera at one equation, review the recognized text,
and return its solution to your app. You can also solve equation text directly.

Open **AresMathScreen** for the supplied AresScan+ style scanner, or use
**AresMathEmbedded** for a camera under your own UI. Both use the same recognition,
review and native solving engine. Your app handles the returned result.

**Package:** `ares_math` v2.0.2 is a self-contained Android/iOS SDK.
Install it from pub.dev; the GitHub repository provides documentation and support,
rather than the SDK implementation. No `ares_edge` package or Edge licence is
required. See [release status](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/release-status.md).

```yaml
dependencies:
  ares_math: ^2.0.2
```

## Choose your scanner integration

**Build your own UI:** embed `AresMathEmbedded`, retain an `AresMathController`,
and connect your own capture, torch, gallery and redo controls. Receive reviewed
results through `onCapture`. Your app owns its layout and navigation.

**Use the provided UI:** call `AresMath.scan` or open `AresMathScreen`
(`AresMathScannerScreen`) for the equation guide, live/digital modes, countdown,
gallery import, manual correction and captured-answer review.

**Solve equation text:** call `AresMath.solve(String)` to receive solution text
with working. This entry point needs neither camera permission nor model weights.

### 1. Capture one equation

Hold the full equation steady and follow the countdown, or disable automatic
capture and use your own capture button. Motion, stale observations or changed
equation text cancel the countdown. See [the supplied scanner](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/scanner-screen.md).

### 2. Review the equation and answer

The screenshots below show actual compiled consumer tests using a synthetic
photograph and configured blue accent/title. They demonstrate the captured-answer
UI and native recognition result; they are not live-camera or accuracy benchmarks.

<img src="https://raw.githubusercontent.com/Ares-Defence-Labs/AresMath/main/media/scanner-android.png" alt="Android Math scanner showing the reviewed x = 2 solution" width="260"> <img src="https://raw.githubusercontent.com/Ares-Defence-Labs/AresMath/main/media/scanner-ios.png" alt="iOS Math scanner showing the reviewed x = 2 solution" width="260">

### 3. Return the result to your app

The supplied route returns an `AresMathScanResult?`; cancellation returns null.
Embedded mode delivers the result through `onCapture` and pauses until
`controller.redo()`. Read `result.equation` and `result.solution` to continue your
own workflow. See [the API reference](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/api-reference.md).

## Scanner appearance, hints and countdown

Set `overlayColor`, `captureTraceColor` and `captureCountdownSeconds` through
`AresMathOptions`. The countdown accepts whole seconds from 1 through 10 (default
3), after stable recognition. It is not a maximum session duration. Both camera
integrations share these options and `autoCapture`, `flashEnabled` and `showOverlay`.

The supplied page also accepts `title`, `backgroundColor`, `borderColor`,
`showGallery`, `showManualEntry` and `showInstructions`. Embedded hosts use
`onScanStateChanged` or `controller.state` for their own hints. See
[all settings and defaults](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/scanner-screen.md).

## Try AresMath in AresScan+

Experience equation scanning in **AresScan+**, the official Ares Defence Labs app.

[![Get AresScan+ on Google Play](https://raw.githubusercontent.com/Ares-Defence-Labs/AresMath/main/branding/google-play-badge.png)](https://play.google.com/store/apps/details?id=ai.aresdefencelabs.aresscan) [![Download AresScan+ on the App Store](https://raw.githubusercontent.com/Ares-Defence-Labs/AresMath/main/branding/app-store-badge.png)](https://apps.apple.com/us/app/aresscan/id6759765449)

[Discover AresScan+](https://aresdefencelabs.com/ares-scan) · [Explore more Ares Defence Labs SDKs](https://aresdefencelabs.com/development-sdks)

## See equation scanning in action

See [visual demos](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/visual-demos.md)
for original screenshots and their test scope. The SDK supplies equation capture
and solution review; the surrounding host app's document editor and sharing
features belong to that app.

## Run the example application

The pub.dev customer package includes an `example/` app for text solving,
the supplied scanner route and a camera embedded under your own controls.
Configure [platform permissions, minimum OS and signing](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/platforms.md)
before running it on a physical device:

```sh
# From the downloaded customer package:
cd example
flutter pub get
flutter run --dart-define=ARES_MATH_LICENCE_KEY=YOUR_PORTAL_ISSUED_KEY
```

Install the package from pub.dev; do not use the documentation repository as a
Flutter dependency. See [example setup](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/example-project.md)
and [performance testing](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/performance-testing.md).

## Documentation

- [Installation and quick start](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/getting-started.md)
- [Embedded camera and custom controls](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/embedded-camera.md)
- [Ready-made scanner](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/scanner-screen.md)
- [Equation text solving and supported mathematics](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/text-api.md)
- [Complete public API reference](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/api-reference.md)
- [Offline licensing, trial and renewal](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/licensing.md)
- [Platform setup and troubleshooting](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/platforms.md)
- [Screenshots and feature scope](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/visual-demos.md)
- [Performance and device testing](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/performance-testing.md)
- [Example application](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/example-project.md)
- [Handwriting model delivery and lifecycle](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/model-delivery.md)
- [Native verification and distribution security](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/security-and-verification.md)
- [Release status](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/release-status.md)

- [Report a bug or ask a question](https://github.com/Ares-Defence-Labs/AresMath/issues)

## Configure your licence

Supply the full signed AMATH2 customer key authorizing `AresMathSDK`, rather than
a portal licence ID or another SDK's key. End users do not enter licence keys.
The configured fee matches AresEdge: US$600 per twelve-month term. One Math
licence covers the scanner and text API across supported apps.

```dart
import 'package:ares_math/ares_math.dart';

await AresMath.configure(
  licenceKey: const String.fromEnvironment('ARES_MATH_LICENCE_KEY'),
);
```

```sh
flutter run --dart-define=ARES_MATH_LICENCE_KEY=YOUR_PORTAL_ISSUED_KEY
```

Keys verify offline. Missing, invalid or expired keys use the shared native
60-second process trial; remounting or configuring the camera does not restart
it. Replace the embedded key in every app before expiry. Never commit a real
key to a repository. Sandbox signatures require a sandbox-trusted test build;
production trust rejects them. See [licensing and renewal](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/licensing.md).

## Ready-made scanner: AresMathScreen

```dart
import 'package:ares_math/ares_math.dart';
import 'package:flutter/material.dart';

Future<AresMathScanResult?> openMath(BuildContext context) => AresMath.scan(
  context,
  licenceKey: const String.fromEnvironment('ARES_MATH_LICENCE_KEY'),
  options: const AresMathOptions(
    title: 'Equation scanner',
    overlayColor: Color(0xFF00BCD4),
    captureTraceColor: Color(0xFFFFB74D),
    captureCountdownSeconds: 4,
    autoCapture: true,
    showGallery: true,
    showManualEntry: true,
  ),
);
```

The route supplies the AresScan+ style page and returns the reviewed result.
For router-owned navigation, push `AresMathScreen` (`AresMathScannerScreen`)
with the same options and key. See [supplied screen and result handling](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/scanner-screen.md).

## Custom camera: AresMathEmbedded

Retain one controller in State, give the camera finite bounds, and remove the
widget before disposing its controller:

```dart
import 'package:ares_math/ares_math.dart';
import 'package:flutter/material.dart';

class EmbeddedMathPage extends StatefulWidget {
  const EmbeddedMathPage({super.key});
  @override
  State<EmbeddedMathPage> createState() => _EmbeddedMathPageState();
}

class _EmbeddedMathPageState extends State<EmbeddedMathPage> {
  final camera = AresMathController();
  String output = '';
  @override
  void dispose() {
    camera.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) => Scaffold(
    appBar: AppBar(title: const Text('My equation scanner')),
    body: Column(children: [
      Expanded(child: AresMathEmbedded(
        controller: camera,
        licenceKey: const String.fromEnvironment('ARES_MATH_LICENCE_KEY'),
        options: const AresMathOptions(
          autoCapture: false,
          overlayColor: Color(0xFF00BCD4),
          captureTraceColor: Color(0xFFFFB74D),
          captureCountdownSeconds: 4,
        ),
        onCapture: (result) => setState(() => output = result.solution),
        onError: (message) => setState(() => output = message),
        onLicenceRequired: () => setState(() => output = 'Math licence required'),
      )),
      FilledButton(
        onPressed: () async {
          try { await camera.capture(); }
          catch (error) { if (mounted) setState(() => output = '$error'); }
        },
        child: const Text('Capture equation'),
      ),
      TextButton(
        onPressed: () async { await camera.redo(); },
        child: const Text('Scan again'),
      ),
      Text(output),
    ]),
  );
}
```

The host owns navigation, system UI and controls. Successful capture pauses
until `redo()`; callbacks do not pop the host route. Only one Math camera can
be mounted at a time. See [embedded controls and lifecycle](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/embedded-camera.md).

### Gallery import

The supplied page includes gallery import; `showGallery: false` hides its button.
Embedded hosts call `controller.pickGallery()` and receive the reviewed equation
through the same result callback. Check camera readiness and catch command errors.
See [gallery and controller reference](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/api-reference.md).

## Model and asset protection

AresMath includes its native solver, licence verifier, camera, printed Latin OCR
and inference runtime. Proprietary native implementation is compiled; public Dart
adapters expose the documented API. Optional CoMER handwriting weights form a
7,593,285-byte store-managed pack. These open third-party weights and their
licence are separate from the proprietary Math engine.

Configure the host application's normal Google Play/Apple resources for
handwriting. A dependency cannot upload store-hosted resources for another app.
The SDK checks pack files against pinned hashes before use. Reviewed package
inventories detect unexpected changes; compiled code cannot prevent a host that
controls the process from inspecting binaries or memory. See
[model delivery](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/model-delivery.md)
and [security boundaries](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/security-and-verification.md).

## Platform requirements

Android API 24+ (compile SDK 36), iOS 16+, Flutter 3.44+, Dart 3.12.2+.
The text API is part of the native Flutter plugin on Android/iOS. This release
does not include desktop, web or command-line Dart production solving. Text-only
calls need no camera permission. See [platform setup](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/platforms.md).

## Equation recognition and text solving

Camera capture recognizes one equation, offers correction when needed, and runs
the same native solver as the direct text API. No photograph or equation is sent
to a remote solving service.

```dart
final String output = AresMath.solve('2x + 3 = 7');
// Solution: x = 2, followed by working.
```

Arithmetic, linear equations in x, real quadratic equations in x, and simple
two-variable linear rearrangement are supported. Other mathematics requests
manual review. Numeric answers are rounded to three decimal places; maximum
input is 4096 UTF-8 bytes. Review recognized equations and answers before use.
See [text API, output format and limits](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/text-api.md).

### Supported public API

Import `package:ares_math/ares_math.dart` for `AresMath`, `AresMathEmbedded`,
`AresMathController`, `AresMathScreen`, `AresMathScannerScreen`, `AresMathOptions`,
`AresMathScanResult`, scanner state/display types, model lifecycle and licensing
models. Internal helper paths and native channels are private. See the
[complete API reference](https://github.com/Ares-Defence-Labs/AresMath/blob/main/docs/api-reference.md).

A commercial licence is required for production use. Downloading documentation,
examples or compiled binaries does not grant a free production licence.
See [LICENSE](https://github.com/Ares-Defence-Labs/AresMath/blob/main/LICENSE).
Third-party components retain their own terms.
