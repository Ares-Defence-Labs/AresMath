# Text-solving API

```dart
await AresMath.configure(licenceKey: mathKey);
try {
  final String result = AresMath.solve('2x + 3 = 7');
  print(result);
} on AresMathLicenceException {
  // Supply a current Math key and configure the SDK again.
}
```

`AresMath.solve(String equation)` returns a String synchronously. Both the camera scanner and this API call the same compiled native solver and licence gate. Text solving does not open a camera, request photo access, download handwriting weights or send equation text to a server.

The API normalizes common OCR typography, including Unicode minus signs, full-width digits/equality and multiplication dots. It selects one equation from multi-line OCR text when possible. Pass one equation per call. An empty input returns an empty string. Inputs containing NUL or exceeding 4,096 UTF-8 bytes throw ArgumentError.

| Input | Solution section |
| --- | --- |
| `2x + 3 = 7` | `x = 2` |
| `x² - 5x + 6 = 0` | `x = 3, x = 2` |
| `y = 2x + 3` | `x = (y - 3) / 2` |
| `2 * (3 + 4)` | `14` |
| `x² + 1 = 0` | `No real solutions` |
| `x - x = 0` | `All real numbers` |
| `x^3 = 8` | Requests manual review |

Output normally includes the equation, a `Solution` section and a `Working` section. Arithmetic-only expressions can return a solution without a working section. The return value is display text, rather than JSON or an exact symbolic AST. Do not parse it as a version-independent machine result schema.

Arithmetic supports decimal constants, parentheses, addition, subtraction, multiplication, constant division, unary signs and powers 0–2. Polynomial solving supports x up to degree two, when intermediate expressions stay within the supported degree. Simple forms such as `y = 2x + 3` can be rearranged. Numerical results use up to three decimal places; results are approximate, not exact rational or symbolic proofs.

Near-zero polynomial coefficients/discriminants and ambiguous floating-point constant equalities request manual review rather than claiming an unreliable root.

General systems of equations, arbitrary variables/powers, calculus, trigonometry, complex roots and general symbolic algebra are outside the v2.0.3 contract. Division by zero and unsupported syntax request manual review; they do not produce invented numerical answers. OCR uncertainty should be resolved by correcting the equation.

After an unlicensed 60-second process-wide trial, solving throws AresMathLicenceException. The gate lives inside the compiled native core and also applies to direct solver calls.
