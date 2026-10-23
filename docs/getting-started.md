# Getting started

Use Flutter 3.44 or later, Dart 3.12.2 or later, Android API 24 or later, or iOS 16 or later. The package is a Flutter plugin; its text API also runs through the native SDK, without opening a camera. Web, Windows, Linux and macOS production support are not included in v2.0.1.

Add `ares_math: ^2.0.1` to `dependencies` in your app's pubspec.yaml and run `flutter pub get`. Configure the signed key after Flutter binding initialization:

```dart
WidgetsFlutterBinding.ensureInitialized();
final status = await AresMath.configure(
  licenceKey: const String.fromEnvironment('ARES_MATH_LICENCE_KEY'),
);
runApp(const MyApp());
```

Ship the full `AMATH2.payload.signature` token in application source or private build configuration. Do not use a portal licence ID, Stripe product ID, API secret, Edge key or Identity key. Build with `--dart-define=ARES_MATH_LICENCE_KEY=...` through private build configuration. Never check a real customer key into a public example.

For text solving, call `AresMath.solve('2x + 3 = 7')`. This is synchronous and returns text. No image/model delivery setup is required for this API.

For scanning, call `await AresMath.scan(context)`, or mount `AresMathScannerScreen` after configuring the SDK. Add the native camera/photo permissions described in [platforms](platforms.md). Configure the handwriting asset pack as described in [model delivery](model-delivery.md) before relying on handwritten input.

Missing or invalid keys do not throw during configuration: inspect `status.licensed` and `status.trialRemaining`. Once the trial expires, solving throws `AresMathLicenceException` and native scanning stops. A valid current Math key authorizes both entry points.
