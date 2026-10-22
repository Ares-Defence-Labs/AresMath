# Release verification — 2.0.0

The standalone customer artifact passed Android and iOS consumer builds and device integration tests. Both platforms verified native text solving, printed-image OCR, the captured-answer review UI, Boolean tensor transport, and the shared 60-second trial expiring without reset after configuration. iOS additionally executed the real store-resolved CoMER handwriting model and solved the recognized equation. Android's handwriting payload was verified by manifest and native runtime checks; an actual Google Play-hosted download remains a host release acceptance step.

The source suite passed 32 tests, including scanner countdown/cancellation, correction, result modes, model lifecycle and configured-key preservation. Isolated Swift and Kotlin probes each passed 19 signed licence cases with fixture trust and rejection against the production pin. Test signing trust and test binaries are excluded from the customer package. Customer native files are audited against their SHA-256 manifest.

The upstream capture-flow handoff passed 62 tests. The standalone checks above are separate evidence.

Actual Google Play/Apple-hosted handwriting downloads require each host application's normal store upload. Local pack/ODR and archive validation cannot establish that store roundtrip. Store-managed handwriting is optional; text solving and bundled printed OCR do not require that pack.

The release is packaged as `ares_math` version `2.0.0`. Check its pub.dev version page for the authoritative publication record. Source and public documentation remain separate repositories.
