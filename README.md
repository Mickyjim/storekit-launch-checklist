# StoreKit Launch Checklist

**Check what happens after someone taps Buy.**

A free checklist for testing subscriptions, lifetime purchases and premium access in an iOS app. Use it when adding in-app purchases or investigating a purchase that did not unlock the expected feature.

For independent developers, small teams and people building with AI assistance. You will need access to your app and its Xcode project to run the checks. This is guidance and test recipes, not an executable test suite or implementation library.

## Start here

1. Check your [product configuration](configuration.md).
2. Run the scenarios below, including the [three detailed test recipes](representative-tests.md).
3. Record what actually happened in the [release evidence worksheet](release-evidence.md). Keep untested items marked **NOT RUN**.

If something fails, use the [diagnostics guide](diagnostics.md) before changing purchase code.

| File | What it helps you do |
| --- | --- |
| [Configuration](configuration.md) | Tell local Xcode test data apart from your real App Store products. |
| [Test recipes](representative-tests.md) | Check subscription expiry, a lifetime refund, and a pending purchase that is later approved. |
| [Diagnostics](diagnostics.md) | Investigate missing products, locked features and access changes. |
| [Release worksheet](release-evidence.md) | Keep local, signed-device and manual test evidence separate. |

<details>
<summary><strong>Open the full purchase and access checklist</strong></summary>

## Before purchase testing

- [ ] Write down product IDs, types, subscription group and feature mapping. Decide whether your app has one access tier or several.
- [ ] Match IDs exactly between your code and configuration. A successful local fixture does not establish App Store readiness.
- [ ] Display StoreKit-provided localized prices. An introductory offer is not necessarily free or available to every customer.
- [ ] Set real Terms and Privacy destinations and a visible restore/manage route.

## Access must be evidence-based

- [ ] Grant access only from verified, recognized transactions and relevant verified renewal information.
- [ ] Keep cancellation, pending approval and verification failure distinct. A purchase callback is not a permanent premium flag.
- [ ] Refresh entitlement evidence at startup/foreground and keep one lifecycle owner for the transaction-update listener.
- [ ] Deliver recognized, verified purchases before finishing them. Do not silently finish unknown products.
- [ ] Check revocation, expiration and superseded transactions. Disabling auto-renew does not immediately end paid access.
- [ ] Evaluate verified billing-grace evidence and its end date. Billing retry alone does not grant access.
- [ ] Do not turn a failed network refresh into a fabricated no-purchase state, or extend an expired grant indefinitely.

## Run this minimum scenario matrix

| Scenario | What to observe |
| --- | --- |
| Fresh install, no purchase | No accidental premium; loading/unknown distinct from a complete empty result. |
| Monthly and annual purchase | Correct localized product; verified access after delivery. |
| Cancel purchase sheet | No new access; existing valid access preserved. |
| Pending purchase | No new grant until verified approval arrives through updates. |
| Relaunch and restore | Known purchases recover; listener not duplicated. |
| Renewal disabled | Access remains until actual verified expiration. |
| Expiration | Observe native expiration before asserting app denial. |
| Lifetime refund | Revocation removes access even though a lifetime purchase has no expiry. |
| Grace, then grace expiry | Access during verified grace; denied after verified grace ends. |
| Billing retry without grace | Retry alone does not grant access. |
| Offline / failed refresh | Explicit uncertainty, bounded existing verified evidence. |

## Repeat beyond local Xcode tests

- [ ] Run your signed app in Sandbox/TestFlight with local StoreKit configuration disabled.
- [ ] Confirm real catalog availability, pricing, groups, offers and relevant account agreements.
- [ ] Check Apple's purchase sheet, restoration, management and your app's access state.
- [ ] Traverse the paywall with VoiceOver, large text, light/dark and reduced-motion/transparency settings.
- [ ] Record toolchain, device/runtime, environment, results and remaining manual checks. A simulator pass does not certify production correctness.

</details>

## Want the implementation too?

**StoreKit Launch Kit is a separate €39 one-time source-code product.** It brings together a StoreKit 2 purchase controller, premium-access rules, three adaptable SwiftUI paywalls, local diagnostics, tests and integration guides.

It fits client-only iOS apps with **one premium access tier**, using auto-renewable subscriptions, a non-consumable lifetime purchase, or both. It does not provide a server, cross-platform accounts, consumable credits or non-renewing subscriptions. Family Sharing is not validated. You still configure your App Store products, signing and legal links, and test your own app on signed devices and in Sandbox/TestFlight, including human accessibility checks.

The 1 October 2026 engineering run recorded 58 core and 14 native StoreKit tests passing for unchanged implementation. These are historical local results, not production certification or a guarantee for your integration.

[Explore the kit, screenshots and commercial terms](https://storekit-launch-kit.favre-michael.chatgpt.site/?utm_source=github&utm_medium=organic&utm_campaign=sklk_founder_01&utm_content=checklist).

This free checklist is useful without buying the kit and contains no paid implementation source. **Disclosure:** Michael Favre owns StoreKit Launch Kit. This resource was prepared with AI assistance.

Apple references: [StoreKit testing walkthrough](https://developer.apple.com/videos/play/wwdc2022/10039/) · [StoreKit 2 overview](https://developer.apple.com/storekit/). Check current API documentation for your deployment target.
