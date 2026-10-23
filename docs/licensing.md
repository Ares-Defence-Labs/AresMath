# Licensing

AresMath is a proprietary commercial SDK from Ares Defence Labs. Both the camera scanner and text API use one Math entitlement. The fee is US$600 per twelve-month prepaid term, covering the customer's apps on SDK-supported platforms. Annual renewal follows the existing SDK licensing system.

| Identifier | Value |
| --- | --- |
| Portal/Stripe metadata product | `math-scanner` |
| Signed product claim | `AresMathSDK` |
| Customer token prefix | `AMATH2` |
| Package | `ares_math` |
| Version | `2.0.2` |

Use the complete signed customer token in AresMath.configure or AresMath.scan, or supply the ARES_MATH_LICENCE_KEY build define. Licence verification runs natively and offline against the pinned issuer. It checks signature, product/prefix, host/customer scope, issue time, annual term/expiry and supported owner bindings. It does not send the key, equation or photograph to a licence server for normal operation.

Without a valid current key, the native process has a 60-second evaluation trial shared by camera and text solving. Configure calls, new widget instances and scanner remounts do not reset it. A new operating-system process starts a new evaluation session; the trial is not a persistent activation counter. After expiry, the text API throws AresMathLicenceException and camera processing/capture stop. A valid Math key authorizes both surfaces.

Edge, Identity, PDF and Office customer keys cannot grant Math access. A signed owner entitlement must explicitly include AresMathSDK and satisfy native application/platform/signer bindings. Use a separate Math owner key when integrating with older SDKs that do not yet recognize a combined grant containing the new Math scope.

Ship a replacement key before annual expiry. Renewing an account does not magically alter a key already embedded in installed apps. Native monotonic timing prevents in-process clock rollback from extending a grant; fully offline cold startup cannot establish trusted UTC against arbitrary device tampering.

Stripe prices are one-time prices for prepaid annual terms. The existing renewal service manages future annual payments; AresMath does not create an extra monthly subscription. Product provisioning does not charge customers. See LICENSE for the commercial terms and SUPPORT.md for assistance.
