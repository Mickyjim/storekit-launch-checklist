# StoreKit release evidence worksheet
Use this with your own app before release. Created by the author of StoreKit Launch Kit; this free worksheet contains no paid kit code. It is a recording aid, not a certification or an executable test suite.

## Identify the build you actually tested
- App/version/build:
- Source revision or artifact checksum:
- Test date and timezone:
- Xcode/Swift versions:
- Device and OS:
- Environment: Xcode-local / signed Sandbox / TestFlight
- Local StoreKit configuration enabled or disabled:
- Tester:

Keep account credentials, receipts, transaction identifiers and customer messages out of a public copy. Record only the minimal state needed to reproduce a failure.

## Capture evidence, not a tick alone
Use PASS only after observing the expected result. Use FAIL for a contradiction, BLOCKED for an unavailable dependency, and NOT RUN when no execution occurred. A test command that never started is NOT RUN, not PASS. Keep local and signed-device results in separate rows.

| Scenario | Environment/build | Expected behavior | Observed native evidence | Observed app behavior | Result | Evidence location | Retest/action |
|---|---|---|---|---|---|---|---|
| Fresh install | | | | | NOT RUN | | |
| Purchase, cancel and pending | | | | | NOT RUN | | |
| Relaunch and restore | | | | | NOT RUN | | |
| Renewal disabled, then expiration | | | | | NOT RUN | | |
| Lifetime refund/revocation | | | | | NOT RUN | | |
| Verified grace, then grace end | | | | | NOT RUN | | |
| Billing retry without grace | | | | | NOT RUN | | |
| Failed refresh/offline | | | | | NOT RUN | | |

These rows are a starting point; use the [scenario matrix](README.md#run-this-minimum-scenario-matrix) and [test recipes](representative-tests.md) to split purchase variants and record bounded waits. If the native evidence and app state disagree, retain both observations instead of changing the expected result to fit the run.

## Keep manual gates separate
| Gate | Status | Evidence/date | Owner and next action |
|---|---|---|---|
| Own product IDs/types/groups and catalog availability | NOT RUN | | |
| Signed-device purchase and management sheets | NOT RUN | | |
| Human VoiceOver traversal/announcements | NOT RUN | | |
| Intended device sizes and supported OS versions | NOT RUN | | |
| Actual Terms, Privacy and support destinations | NOT RUN | | |

A local simulator pass does not fill these rows. Do not label an untested device or environment supported by evidence from another one.

## Before signing off
- [ ] All failures and blocked checks have an explicit disposition.
- [ ] The release artifact is the build identified above, or its changes have been retested.
- [ ] Public screenshots do not reveal private account or transaction information.
- [ ] Any reliability claim names its tested scope and unresolved checks.

Release decision, reviewer and date:
Open limitations:
Next retest trigger (changed product setup, code, toolchain or observed customer defect):
