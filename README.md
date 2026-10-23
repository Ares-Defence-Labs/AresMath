[![Ares Defence Labs](https://raw.githubusercontent.com/Ares-Defence-Labs/AresMath/main/branding/ares-defence-labs-banner.png)](https://aresdefencelabs.com)

# AresMath

> **Commercial SDK — paid licence required for production use.**
> AresMath is proprietary software from Ares Defence Labs. One Math licence covers the scanner and text API across the customer's supported apps.
> Without a valid key, both share a native 60-second process evaluation trial.
> Purchase and embed a current signed key before deploying to customers, and ship a renewed key before annual expiry.
>
> [Purchase a licence](https://aresdefencelabs.com/development-sdks?sdk=math-scanner&view=overview) · [Commercial licence](LICENSE)

Commercial Flutter equation scanner and text-solving SDK for Android and iOS.

## Choose your scanner integration

**Build your own UI:** use **AresMathEmbedded** with an **AresMathController**. Place the native camera and equation overlays in your own page, connect your capture/torch/gallery/redo buttons, and receive reviewed results through onCapture. The SDK does not pop your route or change its orientation/system bars.

**Use the provided UI:** call **AresMath.scan** or open **AresMathScreen** (**AresMathScannerScreen**). It supplies the AresScan+ style camera page, visible countdown, back/torch, live/digital result modes, gallery, manual correction and captured-answer review.

**Solve equation text:** call **AresMath.solve(String)** to receive solution text with working, without camera permission or a model download.

All three entry points share the same native licence and solver.

## Shared scanner settings

```dart
const options = AresMathOptions(
  overlayColor: Color(0xFF00BCD4),
  captureTraceColor: Color(0xFFFFB74D),
  captureCountdownSeconds: 4,
  autoCapture: true,
  flashEnabled: false,
);
```

Both scanner integrations accept these options. The ready-made page additionally supports a header title, background/card-border colours, and gallery/manual-entry/instruction visibility. Defaults retain the AresScan+ presentation. See [all options](docs/scanner-screen.md).

## Installation and text API

**Current release:** [ares_math 2.0.1](https://pub.dev/packages/ares_math/versions/2.0.1).

```yaml
dependencies:
  ares_math: ^2.0.1
```

```dart
import 'package:ares_math/ares_math.dart';

await AresMath.configure(
  licenceKey: const String.fromEnvironment('ARES_MATH_LICENCE_KEY'),
);
final String output = AresMath.solve('2x + 3 = 7');
// Solution: x = 2, followed by working.
```

## Documentation

| Guide | Contents |
| --- | --- |
| [Getting started](docs/getting-started.md) | Installation and first solve |
| [Embedded camera](docs/embedded-camera.md) | Host-owned layout, controls and callbacks |
| [Scanner screen](docs/scanner-screen.md) | Supplied AresScan+ page, colours and countdown |
| [API reference](docs/api-reference.md) | All public classes, methods and options |
| [Text API](docs/text-api.md) | Supported equations, solution format and limits |
| [Licensing](docs/licensing.md) | Math-specific key, trial, annual renewal |
| [Platforms](docs/platforms.md) | Android/iOS permissions and build requirements |
| [Model delivery](docs/model-delivery.md) | Optional store-managed handwriting pack |
| [Visual demos](docs/visual-demos.md) | Capture/review workflow |
| [Performance testing](docs/performance-testing.md) | Profiling and device acceptance |
| [Example project](docs/example-project.md) | Runnable pub.dev example |
| [Release status](docs/release-status.md) | Verified evidence and remaining store checks |

## Supported mathematics

Arithmetic, linear equations in x, real quadratic equations in x, and simple two-variable linear rearrangement are supported. Other mathematics requests manual review. Numeric answers are rounded to three decimal places; review recognized text and the answer. Maximum input is 4096 UTF-8 bytes.

Printed OCR and native runtime are bundled. Optional CoMER handwriting weights form a 7,593,285-byte store-managed pack; configure your application's normal Google Play/Apple delivery resources. No photograph or equation is sent to a remote solving service.

## Try AresMath in AresScan+

[![Get AresScan+ on Google Play](https://raw.githubusercontent.com/Ares-Defence-Labs/AresMath/main/branding/google-play-badge.png)](https://play.google.com/store/apps/details?id=ai.aresdefencelabs.aresscan) [![Download AresScan+ on the App Store](https://raw.githubusercontent.com/Ares-Defence-Labs/AresMath/main/branding/app-store-badge.png)](https://apps.apple.com/us/app/aresscan/id6759765449)

[Discover AresScan+](https://aresdefencelabs.com/ares-scan) · [Explore the SDKs](https://aresdefencelabs.com/development-sdks)

## Support and releases

This public repository contains documentation, branding and demonstration media. Private implementation, release-bot workflows, native code and credentials remain in AresMathSDK. The runnable example and compiled customer package are distributed on pub.dev.

See [changelog](CHANGELOG.md), [support](SUPPORT.md), [security](SECURITY.md), [contributing](CONTRIBUTING.md), and [third-party notices](THIRD_PARTY_NOTICES.md). Public version tags preserve the matching documentation snapshot.
