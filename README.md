# AresMath

Commercial Flutter equation scanner and text-solving SDK for Android and iOS.
Package `ares_math`, version **2.0.0**. Ares Defence Labs.

AresMath has two entry points into the same licensed, on-device native solver:

- **Camera scanner:** point at one equation, follow the visible countdown, then review a captured result. Gallery input and manual equation correction are included.
- **Text API:** pass equation text to `AresMath.solve` and receive solution text with working. No camera permission or model download is needed for text solving.

```yaml
dependencies:
  ares_math: ^2.0.0
```

```dart
import 'package:ares_math/ares_math.dart';

await AresMath.configure(
  licenceKey: const String.fromEnvironment('ARES_MATH_LICENCE_KEY'),
);
final text = AresMath.solve('2x + 3 = 7');
// 2x + 3 = 7
// Solution
// x = 2
// Working ...

// Within a mounted Flutter widget:
final result = await AresMath.scan(context, countdownSeconds: 3);
if (result != null) {
  print(result.equation);
  print(result.solution);
}
```

The camera and text API require the same **AresMathSDK** entitlement. Customer tokens start with `AMATH2`; another SDK's key does not authorize Math. Production licences cover the customer's supported apps for a twelve-month term, at **US$600/year**. A missing, invalid or expired key uses a native, process-wide **60-second evaluation trial**. Reconfiguration and scanner remounts do not reset it.

Supported solving includes arithmetic, linear equations in x, real quadratic equations in x, and simple two-variable linear rearrangement. Unsupported mathematics requests manual review. Numeric answers are rounded to three decimal places. Review recognised text before using an answer.

The inference runtime is bundled with the native SDK. Optional CoMER handwriting weights are a 7,593,285-byte store-managed pack. Configure your application's Google Play/Apple delivery resources before using handwriting recognition; the SDK does not download model files directly from an arbitrary HTTP URL. Printed OCR and typed equations have separate requirements. See the platform and model guides.

## Documentation

- [Getting started](docs/getting-started.md)
- [Camera scanner](docs/scanner.md)
- [Text-solving API](docs/text-api.md)
- [Complete API reference](docs/api-reference.md)
- [Model delivery and lifecycle](docs/model-delivery.md)
- [Platforms and permissions](docs/platforms.md)
- [Licensing](docs/licensing.md)
- [Example and migration](docs/example-and-migration.md)
- [Security, dependencies and verification](docs/security-and-verification.md)
- [Release status](docs/release-status.md)

[Public documentation](https://github.com/Ares-Defence-Labs/AresMath) · [Ares Defence Labs](https://aresdefencelabs.com) · [Commercial licence](LICENSE) · [Support](SUPPORT.md)
