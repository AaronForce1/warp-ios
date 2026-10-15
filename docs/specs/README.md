# Warp iOS feature map

The [product foundation](product-foundation.md) is the authoritative requirements record. This index groups capability references without duplicating their contracts. Confirmed requirements are distinct from delivered capabilities; no application capability has been implemented.

The [five MVP gap proposals](mvp-gap-proposals.md) provide numbered acceptance clauses for terminal/baseline, performance, recovery/history, agent control and cross-device/account behaviour. These additions await product confirmation and do not replace existing agreements.

| Capability | Authoritative requirements | Related design |
|---|---|---|
| Interactive terminal and Linux workflow baseline | [TERM-01](product-foundation.md#term-01-native-interactive-terminal), [TERM-02](product-foundation.md#term-02-on-device-execution-within-ios-constraints), [TERM-03](product-foundation.md#term-03-remote-and-infrastructure-workflows), [TERM-04](product-foundation.md#term-04-general-linux-environment-baseline), [PERF-01](product-foundation.md#perf-01-responsiveness-is-a-core-acceptance-requirement) | [Runtime boundary](../design.md#proposed-responsibility-boundary) |
| Host connection and preparation | [EXEC-01/02](product-foundation.md#exec-01-connected-execution-is-acceptable-for-the-first-release), [SSH-01/02](product-foundation.md#ssh-01-host-os-independent-ssh-connections), [SETUP-01](product-foundation.md#setup-01-explicit-bring-your-own-server-preparation) | [Runtime/task flow](../design.md#representative-task-flow) |
| Persistent multiple sessions | [SESSION-01/02](product-foundation.md#session-01-preserve-work-across-mobile-interruption-and-relaunch) | [Recovery](../design.md#interruption-and-recovery-proposal) |
| Phone-owned BYOK agent and approvals | [AGENT-01/02/03](product-foundation.md#agent-01-agentic-layer-over-terminal-execution), [AI-01](product-foundation.md#ai-01-bring-your-own-model-credentials-for-mvp) | [Component view](../design.md#proposed-component-drill-down) |
| iCloud app/credential data and device scope | [SYNC-01](product-foundation.md#sync-01-icloud-synchronization-in-mvp), [PLATFORM-01](product-foundation.md#platform-01-iphone-and-ipad-with-app-store-distribution) | [Sync/ownership](../design.md#synchronization-and-device-ownership) |
| Follow-up provisioning and research | [CLOUD-01](product-foundation.md#cloud-01-in-app-provisioning-in-an-early-follow-up-release), [SETUP-02](product-foundation.md#setup-02-optional-later-automatic-setup-through-ssh), [INTEGRATION-01](product-foundation.md#integration-01-assess-warp-account-feasibility), [MODEL-01](product-foundation.md#model-01-later-model-routing-and-switching), [AGENT-CLOUD-01](product-foundation.md#agent-cloud-01-later-cloud-agent-management-research) | [Alternatives](../design.md#alternatives-and-tradeoffs) |

Shared context: [glossary](../GLOSSARY.md), [preferences](../PREFERENCES.md), [roadmap](../ROADMAP.md) and [check contract](../conventions.md). The roadmap owns delivery progress; the feature map does not declare completion.
