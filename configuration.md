# Local configuration versus Sandbox
Local .storekit files are fixtures. They let Xcode provide product metadata and simulated transactions without proving that your real catalog is available. Synced configurations can mirror App Store Connect metadata, but editing local data does not edit your store.

For local tests: select the intended .storekit file in the Run scheme, confirm product IDs/types/grouping, choose predictable scenario settings, and document local prices as sample data.
For signed Sandbox checks: choose None for the scheme's StoreKit Configuration and use your authorized Sandbox setup. Verify the real app bundle, products and account agreements. Never ask buyers to share Apple signing keys.

Small diagnostic example (pseudocode):
```
expectedIDs = IDs declared by this app
returnedProducts = await loadProducts(expectedIDs)
missingIDs = expectedIDs minus IDs(returnedProducts)
if missingIDs is not empty:
    show a retryable store-unavailable state
    record only missing product IDs and environment in local diagnostics
    preserve unrelated valid entitlement evidence
```
Do not hardcode prices or grant access to compensate for missing products.

Reference: https://developer.apple.com/videos/play/wwdc2022/10039/ (environment/configuration walkthrough). API details and menu names may vary by Xcode version.
