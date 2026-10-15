# Warp iOS project records

The MVP is a native iPhone/iPad terminal client for user-prepared SSH hosts, with phone-owned BYOK agent coordination, persistent multi-session remote execution, iCloud sync and an App Store release target. These are requirements and planning records; no application has been implemented.

- [Product foundation](specs/product-foundation.md): authoritative requirements, agreement, current questions and claim-level readiness review.
- [Proposed MVP acceptance requirements](specs/mvp-gap-proposals.md): five numbered gap proposals and acceptance examples for product confirmation.
- [Feature map](specs/README.md) and [glossary](GLOSSARY.md): capability navigation and shared meanings.
- [Runtime architecture](design.md): native/runtime/synchronization boundaries, source mappings and feasibility limits.
- [Project preferences](PREFERENCES.md): user preferences, delegated technical direction and tooling applicability.
- [Roadmap](ROADMAP.md): current planning/delivery state, future scope and resume point.
- [Draft MVP phases](phases/mvp.md): tasks, dependencies, closing evidence and counterexamples.
- [Check contract](conventions.md): planned required gates, scope, evidence and unconfigured-tool limitations.
- [iOS execution research](research/ios-execution.md): platform, remote-session and agent-runtime evidence.
- [Native, Expo and sync research](research/native-stack-and-sync.md): current candidate/service/API evidence and unvalidated operations.
- [Warp-account feasibility](research/warp-account-feasibility.md): documented cloud-run integration and unresolved phone-inference/mobile-login scope.

The repository's [workflow](../.claude/skills/_shared/development-workflow.md) and [delivery contract](../.claude/skills/_shared/delivery-contract.md) govern handoffs. Product agreement, successful builds/tests, implementation completion and publication are distinct states.
