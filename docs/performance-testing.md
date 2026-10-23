# Performance testing

Benchmark the supplied screen and embedded widget on the Android/iOS devices you support. They share the same native camera, OCR, handwriting runtime, solver and licence gate. Neither API includes a claimed FPS or model-accuracy guarantee.

Use the example to compare cold camera startup, first model activation, warm recognition, manual capture, automatic countdown and repeated redo. Measure printed and handwritten equations separately. Include small screens, landscape host layouts for embedded mode, app background/resume, torch, permission denial, and model removal while a reader is active.

Record frame/build timings using Flutter profiling tools. The embedded state callback can run during live observations; update only the host UI that needs changing. Do not write every OCR frame or photograph to production logs. Disable autoCapture to compare manual capture; hiding overlays does not disable inference.

Model delivery can outlive the first photograph. The scanner rechecks fresh observations before automatic capture and cancels stale countdowns. Store-hosted download performance must be measured in a normal Play/App Store distribution, separate from local test/ODR evidence.

The release workflow verifies native library 16 KiB alignment. Its device receipt records the actual Android page size; a 4 KiB emulator run is not presented as a 16 KiB runtime test. See [release evidence](release-status.md).
