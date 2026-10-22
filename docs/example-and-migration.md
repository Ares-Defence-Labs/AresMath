# Example and migration

The example demonstrates both supported entry points: a text field calling AresMath.solve and a button presenting AresMath.scan. Run flutter pub get in example, configure your Math build define, then build/run the Android or iOS app. Text solving and printed capture do not require handwriting weights. For handwriting, include/upload the model resources using the model-delivery guide.

The supplied scanner preserves the completed AresScan capture-flow revamp: stable detection, visible countdown, frozen capture, reading progress, manual correction, retake, live-answer/digital-result modes and persistent review. Scanner routing, gallery selection, loading indicator, native camera and solver now belong to AresMath rather than the AresScan application.

Replace app-private inkMath imports with package:ares_math/ares_math.dart. Replace InkIntelligenceProcessor.solveMath with AresMath.solve. Replace host-specific route pushes with await AresMath.scan(context), or mount AresMathScannerScreen in your router. Configure a Math key independently from other SDK keys. Existing source-level InkMath aliases are retained privately for owner migration; use AresMath names in customer integrations.

The SDK returns the equation, solution, chosen mode and optional source image path. Your app owns persistence, sharing, notes, analytics and document export. Avoid opening multiple cameras simultaneously. Rebuild native targets after adding the plugin; hot reload cannot register native plugins or replace licence verifier binaries.
