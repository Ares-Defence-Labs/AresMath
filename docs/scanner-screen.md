# Ready-made scanner screen

`AresMath.scan` opens the supplied AresScan+ style route and returns an `AresMathScanResult?`. Cancellation returns null. It includes back/torch, equation guide, visible countdown, live/digital modes, capture, gallery, correction, redo and solution review.

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

Use `Navigator.push<AresMathScanResult>` with `AresMathScreen` (an alias for `AresMathScannerScreen`) if your router owns route creation. Both accept options, licenceKey, initialImagePath and initialEquation. The legacy countdownSeconds argument remains supported and overrides options.captureCountdownSeconds when supplied.

The default layout, dark cards, captured-result state and review controls follow AresScan+. The supplied route owns its full-screen presentation and portrait orientation while mounted. Use the embedded widget for your own layout/navigation. Color values are Flutter Color/ARGB values, including alpha.

| Setting | Default | Effect |
| --- | --- | --- |
| overlayColor | 0xFF7FE6C5 | Answer overlay, accent icons, selected mode, main actions |
| captureTraceColor | null | Countdown guide border; null follows overlayColor |
| backgroundColor | black | Route background |
| borderColor | 0xFF4B4D51 | AresScan-style card borders |
| title | Ink Math | Header text |
| captureCountdownSeconds | 3 | Stable-equation countdown, 1–10 whole seconds |
| autoCapture | true | Automatic countdown/capture; false uses Solve |
| flashEnabled | false | Initial torch request |
| showOverlay | true | Guide/answer graphics |
| initialDisplayMode | liveOverlay | Initial answer presentation |
| showGallery | true | Gallery control |
| showManualEntry | true | Enter-equation control |
| showInstructions | true | Instruction card on sufficiently tall layouts |

The capture options apply to embedded and route integration. The header, instructions and action visibility settings apply only to the supplied route. Rebuilding updates styling, visibility and automatic countdown settings; a countdown-duration change or disabling auto capture cancels a pending countdown. Initial flash, display mode and input values are mount-time settings.

Only Math-relevant options are exposed. Edge document shape, perspective extraction, grid and document-size settings do not apply to equation recognition. Matching names such as overlayColor, captureTraceColor, autoCapture, captureCountdownSeconds and flashEnabled follow the Edge SDK convention.

See [embedded camera](embedded-camera.md), [API reference](api-reference.md), and [platform setup](platforms.md).
