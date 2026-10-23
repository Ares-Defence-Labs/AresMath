# Example project

The runnable Flutter example ships in the [ares_math package](https://pub.dev/packages/ares_math/example); this repository follows AresEdge's documentation-only structure. It contains guides, branding and demonstration media, while private source, CI, native builds and signing material remain in AresMathSDK.

Download the package archive from pub.dev, extract it and open its example directory. Regenerate standard Flutter host wrappers omitted automatically by pub.dev:

```sh
flutter create --platforms=android,ios --project-name=ares_math_example .
flutter pub get
flutter run --dart-define=ARES_MATH_LICENCE_KEY=YOUR_SIGNED_MATH_KEY
```

The example demonstrates typed text solving, the configurable supplied route and an embedded camera under host-owned controls. Replace the placeholder key in your private build configuration; production SDKs reject sandbox issuer keys.

Keep the example's tagged Apple handwriting resources and Android pack configuration when regenerating hosts. Confirm bundle/package IDs, camera permission strings, minimum platform versions and your application's normal store asset delivery configuration. See [platforms](platforms.md) and [model delivery](model-delivery.md).

The packaged integration harness verifies compiled text solving, Boolean tensor transport, printed-image OCR, captured-result review, embedded callbacks/navigation ownership and shared native trial expiry. iOS additionally runs actual CoMER inference against the locally resolved ODR pack. These checks do not establish an actual store-hosted download roundtrip.
