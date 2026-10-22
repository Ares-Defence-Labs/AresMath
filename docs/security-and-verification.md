# Security, dependencies and verification

The licensed solver and native camera/licence implementation are compiled in the customer distribution. Public Dart code provides typed adapters, capture UI, recognition orchestration and model lifecycle. Native camera frame/capture checks and the synchronous solver each enforce the Math entitlement/trial. A Dart callback cannot override native denial. Platform/issuer pins are separated from isolated sandbox test builds.

Normal equation recognition and solving run on device. App installation/build dependency resolution and store-managed handwriting model delivery can require network access. Printed Latin OCR and native text solving are bundled. No claim of zero network activity during first installation or asset download is made. Captured equations are not uploaded for inference by this SDK.

Handwriting uses third-party CoMER quantized model files and vocabulary, retained with their Apache-2.0 licence. ONNX Runtime, its Flutter adapter and other dependencies retain their applicable notices. THIRD_PARTY_NOTICES.md identifies the shipped components. Public CoMER model files are not represented as secret proprietary model weights.

Verification includes public text API cases, unsupported input and bounds, native authorization denial, scanner countdown/cancellation and persistent result layouts, conservative OCR/crop tests, model checksum/caching/removal/re-download, isolated native signed-key vectors and rejection of synthetic keys by production trust. Android/iOS consumer builds verify package linkage. See release-status.md for the exact release evidence and remaining host-specific store checks.

Native checks raise the cost of bypassing licensing but do not make a client executable unmodifiable. Do not publish signing secrets, real customer keys, sandbox-trusted binaries or private implementation source. Report reproducible vulnerabilities privately using SECURITY.md.
