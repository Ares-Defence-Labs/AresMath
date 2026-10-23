# Changelog

## 2.0.3 — 2026-10-23

- Redesign the supplied scanner around a full camera preview with transparent top controls, 15% larger back/flash buttons, a compact status pill, corner guides and an Ink Math footer.
- Show equation detection and a visible capture countdown with a working Cancel action; cancelled equations remain available for manual capture without restarting the timer.
- Use a black capture symbol on the white shutter and preserve equation correction, gallery, result review and embedded scanner integration.

AresMath v2.0.3

## 2.0.2 — 2026-10-23

- Document host JNI packaging when Math and another native SDK both bundle the shared C++ runtime.

- Acknowledge only Pub’s exact docs-directory naming warning after full validation; fail on every other warning or validation error.

- Publish the common SDK documentation layout and complete integration examples in the v2.0.2 customer package.

- Document authenticated retry timing and operational recovery without editing release records.

- Update release evidence documentation for the current Worker and Python verification suites.

- Measure resumed release verification against the authenticated current workflow attempt instead of the original reservation time.

- Read the documented Math licence build define in the runnable example and remove its stale version label.

- Match the AresIdentity documentation header and section order, with complete route, embedded-camera and text API examples.

- Hold a temporary Mac sleep assertion only while native release checks run and release it on success or failure.
- Keep generated example CocoaPods self-version metadata out of source attestation and preserve resolved source/consumer pod locks as release evidence.
- Restore the isolated publication dependency cache after setup-dart and report any unexpected dirty-source paths.

AresMath v2.0.2

## 2.0.1 — 2026-10-22

- Add AresMathEmbedded and AresMathController for host-owned camera layouts and capture/result callbacks without SDK navigation.
- Add AresMathScreen and shared AresMathOptions for AresScan+ style routes with configurable colours, countdown, auto capture, torch and controls.
- Connect the Math SDK to the scoped release bot, private native verification, pub.dev publication and documentation-only public releases.
- Align public documentation, branding, examples and guide structure with AresEdge; bind customer receipts to pub.dev's actual file inventory.

- Constrain configured scanner titles on narrow displays after compiled iOS layout verification.

- Harden disposable release devices and preserve readable release evidence and upload-attempt receipts.

- Upgrade Android licence cryptography to Bouncy Castle 1.86 and verify resolved runtime dependencies against security advisories.

- Keep canonical and compatibility API guides on the same automatically allocated release version.

- Enable registered-tag automated publication after the native release gates and independent registry verification.

- Verify the compiled Android consumer on a 16 KiB Android 35 emulator; release completed Android test resources before iOS acceptance and refresh the iOS scanner preview.

AresMath v2.0.1

## 2.0.0

- Extract the completed Math scanner into the standalone AresMath SDK.
- Supply a camera route with stable countdown, capture/loading states, correction, retake and persistent review.
- Add the synchronous text API with the same compiled native solver.
- Enforce Math-specific signed licences and a shared native 60-second process trial.
- Include verified store-managed handwriting model download/removal APIs.
- Document installation, public APIs, supported mathematics, model delivery, commercial licensing and migration.
