# Embedded equation camera

Use `AresMathEmbedded` when your application owns the page, toolbar and navigation. It contains the native camera and equation guide/answer overlays, with no SDK Scaffold or toolbar. Give it finite width and height. Keep one controller for the widget's lifetime; remove the widget before disposing its controller. Only one Math scanner can be mounted at a time.

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

Configure a key once with `AresMath.configure` instead if several SDK entry points share it; omitting the widget's key preserves that configuration. An explicitly supplied widget key is configured before its camera starts. The key is a mount-time setting; recreate the widget or call configure explicitly to replace it.

A successful capture calls `onCapture` once and pauses on the captured image. Call `redo()` to release that result and scan another equation. It never pops the host Navigator, changes orientation, or applies full-screen system bar settings. Unsupported mathematics requests manual review; recognition is not a guarantee that an equation is solvable.

`autoCapture: true` starts the configured countdown only after stable equation observations. Motion, stale observations or changed equation text cancel it. `false` keeps recognition active while requiring controller capture. `showOverlay: false` hides guide/answer graphics without disabling recognition.

The default correction dialog is supplied when text needs review. Supply `reviewEquation: (detected, alternatives) async => ...` to show your own editor and return corrected text, or null to cancel. The host must still provide a Material/Navigator context for the default dialog/gallery interaction.

`onScanStateChanged` and `controller.state` expose phase, countdown, equation, error and captured result. `controller.isAttached` indicates attachment; commands also require completed initialization. Catch StateError for commands made before attachment/initialization, after disposal, or while another command is pending. Scanner/recognition errors are delivered through onError/state. Trial expiry invokes onLicenceRequired once and prevents further capture.

See [shared options and API reference](api-reference.md), [model delivery](model-delivery.md) and [performance testing](performance-testing.md).
