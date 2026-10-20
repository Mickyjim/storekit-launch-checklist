# StoreKit Launch Checklist
A practical checklist for the gap between a purchase button and reliable access. A free resource from the owner of StoreKit Launch Kit, prepared with AI agents. No paid kit source is included.

## Before purchase testing
- [ ] Write down your product IDs, product types, subscription group and feature mapping. Decide whether you have one access tier or several.
- [ ] Confirm IDs match your code exactly; distinguish local StoreKit configuration from App Store Connect. A successful local fixture does not establish store readiness.
- [ ] Display StoreKit-provided localized prices. Do not infer an introductory offer is free or available to every customer.
- [ ] Set real Terms and Privacy destinations and a visible restore/manage route.

## Access must be evidence-based
- [ ] Grant access only from verified, recognized transaction evidence and relevant verified renewal information.
- [ ] Handle cancellation, pending approval and verification failure distinctly. A purchase callback is not a permanent premium flag.
- [ ] Refresh current entitlement evidence at startup/foreground and keep a transaction-update listener alive under one lifecycle owner.
- [ ] Deliver recognized verified purchases before finishing them. Do not silently finish unknown products.
- [ ] Check revocation, expiration and superseded transactions. Subscription auto-renew disabled does not mean access ends immediately.
- [ ] If using billing grace, evaluate verified grace evidence and its end date. Billing retry alone is not an entitlement.
- [ ] Do not convert a failed network refresh into a fabricated no-purchase state. Do not extend an expired grant indefinitely.

## Run this minimum scenario matrix
| Scenario | What to observe |
|---|---|
| Fresh install, no purchase | No accidental premium; loading/unknown distinct from complete empty result |
| Monthly and annual purchase | Correct localized product; verified access after delivery |
| Cancel purchase sheet | No new access; existing access preserved |
| Pending purchase | No new grant until verified approval arrives through updates |
| Relaunch and restore | Known purchases recover; listener not duplicated |
| Renewal disabled | Access remains until actual verified expiration |
| Expiration | Native expiration is observable before app denial is asserted |
| Lifetime refund | Revocation removes access despite absence of subscription expiry |
| Grace then grace expiry | Access during verified grace, denied after verified grace end |
| Billing retry, no grace | Retry alone does not grant access |
| Offline / failed refresh | Explicit uncertainty, bounded existing verified evidence |

## Repeat beyond local Xcode tests
- [ ] Run your signed app in Sandbox/TestFlight with local StoreKit configuration disabled.
- [ ] Confirm actual catalog availability, pricing, groups, offers and relevant account agreements.
- [ ] Check Apple's purchase sheet, restoration, management and app-specific entitlement state.
- [ ] Traverse paywall with VoiceOver, large text, light/dark and reduced-motion/transparency settings.
- [ ] Record toolchain, device/runtime, environment, result and outstanding manual checks. No claim of universal production correctness follows from a simulator pass.

See [diagnostics](diagnostics.md), [test recipes](representative-tests.md), [configuration](configuration.md) and the [release evidence worksheet](release-evidence.md). Copy the worksheet for your own build; its unrun rows stay NOT RUN until supported by observations.

## Need the implementation too?
Disclosure: StoreKit Launch Kit is my separate paid source-code product, **€39 one-time**. It is for a client-only iOS app with one premium access tier using subscriptions, lifetime access, or both. The package includes three replaceable paywalls, an entitlement policy and diagnostics. The 1 October engineering run recorded 58 core and 14 native tests passing; these are historical results for unchanged implementation, not production certification.

This checklist remains useful without buying the kit. It contains no paid kit source. If you need a server-authoritative entitlement service, cross-platform accounts or a consumable ledger, this package does not provide them. Family Sharing is not validated. Your own App Store configuration, signing, signed-device Sandbox/TestFlight and human accessibility checks remain necessary.

[Screenshots, scope and commercial terms](https://storekit-launch-kit.favre-michael.chatgpt.site/?utm_source=github&utm_medium=organic&utm_campaign=sklk_founder_01&utm_content=checklist).

Apple references: [StoreKit testing walkthrough](https://developer.apple.com/videos/play/wwdc2022/10039/), [StoreKit 2 overview](https://developer.apple.com/storekit/). Check current API documentation for your deployment target.
