# Diagnose before rewriting purchase code
Use this table when a developer reports “StoreKit purchase succeeds but the subscription is not active.” First write down the environment (local StoreKit configuration, Sandbox, TestFlight or production), product ID and type, the app's observed purchase result, and whether the current entitlement read completed. Do not paste receipts, transaction identifiers, customer information or credentials into a public issue.

Five-minute triage:
1. Confirm the button is offering the intended product in the intended environment. Local fixture success does not prove that App Store Connect products are available.
2. Separate the purchase result from access evidence. Pending, cancelled and unverified outcomes do not grant access; a successful callback alone is not the final entitlement policy.
3. Check whether the recognized, verified transaction reaches the app's gate through refresh or the transaction listener. Record whether that read is complete, loading or failed.
4. If access existed previously, inspect expiration, grace end, revocation and upgrade/supersession before resetting state. Cancellation of renewal does not instantly revoke paid time.
5. Reproduce with a signed Sandbox/TestFlight app and local StoreKit configuration disabled before asserting live-store behavior.

| Symptom | First distinction | Action | Passing evidence |
|---|---|---|---|
| Products empty | Local config vs Sandbox | Check scheme config and exact IDs; in Sandbox check store product readiness/availability/account configuration | Expected IDs returned in intended environment |
| Purchase succeeds, feature locked | Purchase result vs verified access state | Inspect verification, catalog mapping and refresh/listener delivery | Verified recognized evidence reaches gate |
| User cancels, old access disappears | Purchase UI outcome vs existing entitlement | Separate cancelled attempt from entitlement refresh | Existing valid entitlement retained |
| Annual expiry test flaky | Test session mutation vs native observed expiration | Disable renewal, advance test time, poll native and app observations with deadline | Native expiry and app denied access both observed |
| Access lost during grace | Transaction expiration vs grace boundary | Inspect verified renewal grace data; do not grant for billing retry alone | Access until verified grace end |
| Refund doesn't remove lifetime | Duplicate transaction ID vs changed revocation | Re-evaluate updated transaction evidence, including revocation | Same transaction can revoke prior grant |
| Restore appears broken | No product history vs auth/error/refresh | User-triggered sync then read evidence; show error separately | Known test purchase recovers after relaunch |
| Works locally, fails TestFlight | Fake local fixture vs real catalog | Disable scheme config, inspect actual account/product setup | Signed Sandbox/TestFlight observed behavior |

Do not log raw transaction payloads, customer identifiers or credentials in public bug reports.
