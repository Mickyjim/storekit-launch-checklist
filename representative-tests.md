# Three representative test recipes
These are implementation-neutral test specifications, not copied kit tests or an executable test suite. Adapt to your own controller and current StoreKitTest API. They do not add to the paid kit's 72-test count.

## 1. Expiration after renewal is disabled
Given a clean local StoreKitTest session and recognized annual subscription, purchase and wait for verified access. Disable renewal and accelerate the test session's time. Poll native transaction evidence until expiration is at/before the observation clock, with a fixed deadline. Refresh the application and assert denied access. On timeout record native expiration and app state separately. Never replace the assertion with an arbitrary sleep or manually force premium=false.

## 2. Refund of lifetime access
Purchase a recognized non-consumable, wait for verified access, then simulate its refund in the local transaction manager/session. Wait for verified revoked evidence and assert access is removed. Relaunch and assert it stays removed. Include a regression where the updated transaction retains the same transaction identifier; event deduplication must not discard the revocation.

## 3. Pending then approved
Enable interrupted/pending purchase behavior in the local test environment. Start purchase; assert no new entitlement from pending alone. Resolve the purchase in the test environment, then observe the long-lived update listener. Assert access appears only after verified delivery. Existing unrelated valid entitlements should survive the pending attempt.

Every test must reset its own local state, use bounded waits and fail with useful state evidence. Do not alter a real customer's purchases. Retest signed Sandbox/TestFlight separately.
