# Camera scanner

```dart
final AresMathScanResult? result = await AresMath.scan(
  context,
  licenceKey: const String.fromEnvironment('ARES_MATH_LICENCE_KEY'),
  countdownSeconds: 3,
);
```

Point at one complete equation. The scanner combines native camera OCR, periodic high-resolution snapshots, conservative candidate selection and optional on-device handwriting recognition. A stable equation starts a visible countdown. Movement, changed/stale recognition or disappearance cancels pending capture. Capture freezes the photograph, shows reading/solving progress and keeps the result visible for review. Users can correct the equation, enter one manually, select an image, retake and return a result.

`countdownSeconds` accepts integers 1–10 and defaults to 3. It controls the stable-detection countdown, rather than a maximum scanner-session duration. Licence expiry remains independent. The SDK uses its own native camera view and channel namespace, and does not depend on the Edge or Live Text SDK.

`AresMath.scan` installs an explicitly supplied key; otherwise it preserves an already configured key or initializes the build-defined key. It pushes a Material route on the supplied context's Navigator. The returned future completes when the user accepts the result or leaves the scanner. Cancellation returns null. Do not open concurrent scanner sessions on the same Flutter engine.

To place the screen in your navigation system, configure the SDK first, then use:

```dart
const AresMathScannerScreen(
  initialImagePath: null,
  initialEquation: null,
  countdownSeconds: 3,
);
```

`initialImagePath` opens an existing encoded image; `initialEquation` opens an already recognised equation in digital-result mode. A supplied initial equation is still evaluated by the licensed native solver.

The two display modes are `AresMathDisplayMode.liveOverlay` and `AresMathDisplayMode.digitalResult`. Both use the same equation/solution contract. The live answer is a UI overlay; `sourceImagePath` identifies the captured/imported source image and is not a promise of a permanently exported image containing an answer overlay.

A result contains `equation`, `solution`, `displayMode` and nullable `sourceImagePath`. Paths created by capture can be temporary. Copy any required image to your application's permanent storage. The SDK returns results to your app; saving, sharing, editing notes and document export are application features.

If the handwriting pack is unavailable, still capture can fall back to native printed-text OCR with mandatory equation confirmation. Unreadable input still needs correction or the configured handwriting pack.

The camera screen displays licence-trial expiry and stops the camera stream. Previously captured results can remain visible for review; new solving stays subject to the native gate. Reopening the scanner does not restart the native trial.
