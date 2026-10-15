# Warp iOS roadmap

**Current scope:** Agent-owned discovery, architecture, and planning for a new iOS application; the human confirms product requirements.
**Understand status:** Clarification ongoing — the current claim-level review is in [the product foundation](specs/product-foundation.md#readiness-review).
**Planning status:** Planning in progress; the [draft MVP phase plan](phases/mvp.md) has closing tasks and evidence, but native/host feasibility and remaining sync scope are unresolved.
**Owner:** Codex coordinates technical work and maintains these records.

## Current records and next decision

[Product foundation](specs/product-foundation.md) owns confirmed direction and unresolved product choices. The primary outcome is confirmed: a responsive interactive terminal with a minimal Debian/Ubuntu-like environment and an agentic layer. Native on-device execution is preferred; a personal-computer/cloud backend may be considered. First-release connectivity has been explicitly accepted. MVP onboarding uses an existing server/computer, with repository-maintained scaffolding and cloud-init. In-app cloud provisioning is deferred from MVP and planned for version 1.1 or 1.2. Host OS is not restricted: SSH compatibility defines the connection scope. Direct password/key authentication is agreed; bastions, SSH MFA and forwarding are outside MVP. iPhone/iPad, App Store distribution, and iCloud sync are launch requirements. A dashboard without terminal interaction would not satisfy the direction.

**Next product review:** the [five numbered MVP acceptance proposals](specs/mvp-gap-proposals.md) are drafted for group-by-group or clause-level confirmation. Their performance/retention defaults and control/account behaviours are proposed, not silently added to agreed scope.

A final discovery scan identified two additional agent-control details, now proposed in **4.6** (AI context/disclosure) and **4.7** (elevated/destructive-action approval). These are unconfirmed additions within group 4, not new implemented capabilities. The five groups still await decisions; subsequent native/provider/host research remains agent-owned.

## Work sequence

| Stage | Current state | Work and completion evidence |
|---|---|---|
| Understand | In progress | Interview through product decisions, inspect relevant integration facts, record capabilities and acceptance examples, challenge material claims, and obtain product agreement. |
| Design | In progress; runtime division agreed and native/sync boundaries proposed | Select the stack under delegated authority; describe responsibilities, C4 views, code mappings, contracts, important flows and failures; record evidence limits and verification obligations. |
| Plan Delivery | Draft phases recorded; coverage review in progress | [MVP phases](phases/mvp.md) connect the agreed scope to tasks, dependencies, counterexamples and closing evidence. Credential sync is agreed; raw terminal retention, recovery and native/host feasibility remain unresolved. On-device Linux execution is a later goal, not an unresolved MVP prerequisite. |
| Implement / Verify / Review | Future delivery scope | Use the corresponding skills once there is an actionable plan and an implementation request. No application work or checks have been performed. |

## Discovery tasks

- [x] Confirm the primary direction: native interactive terminal plus agentic layer. First-release sequencing remains open.
- [x] Confirm that the first release may require a connection to the execution environment.
- [x] Confirm bring-your-own host for MVP, plus repository server scaffolding and cloud-init.
- [x] Confirm SSH compatibility, rather than host OS, as the connection boundary.
- [x] Confirm session preservation across mobile suspension, app termination/relaunch, and network disconnection.
- [x] Confirm multiple named persistent sessions across saved hosts; switching sessions must not interrupt work.
- [x] Confirm MVP existing-host onboarding: user-run repository setup script and in-app prerequisite instructions.
- [x] Confirm direct password/key SSH; bastions, SSH MFA and port forwarding are outside MVP.
- [x] Confirm iPhone/iPad and App Store distribution, with native-component preference and Expo distribution investigation.
- [x] Confirm iCloud sync is an MVP requirement.
- [x] Confirm SSH credential and model-provider key synchronization through iCloud Keychain in MVP.
- [x] Draft initial requirements and acceptance examples for the five remaining gap groups, clearly separating proposals from agreements.
- [ ] Obtain product decisions on the numbered gap proposals and reconcile affected records/readiness claims.
- [ ] Define raw terminal retention, account/unavailable-sync behaviour and supported preparation/connection failure outcomes.
- [x] Confirm user-selectable task-level and per-command agent approval.
- [x] Confirm BYOK for MVP AI; Warp-account access is not required for that path.
- [x] Agree MVP runtime: phone-owned agent coordinator/provider credentials; persistent terminal commands execute remotely.
- [ ] Define continuation-setting and recovery UX across iOS suspension/termination, without promising always-on phone execution.
- [x] Confirm launch providers: OpenAI, Anthropic, DeepSeek, and Qwen; no other must-have providers identified.
- [ ] Validate provider endpoint/model/tool-call compatibility and define agent task boundaries, credential/preference lifecycle, and failure/recovery behaviour.
- [ ] Investigate facts underlying any proposed integration before making guarantees.
- [ ] Reconcile the saved requirements, acceptance examples, and readiness review.
- [ ] Produce the architecture and reviewed delivery plan within the requested scope.

## Draft MVP phase sequence

| Phase | Observable outcome | Dependency / current state |
|---|---|---|
| P0 | Native/host/provider/sync contract feasibility | Planned validation; documentation research completed, no native prototype. |
| P1 | Prepare a baseline host and use the first native terminal | P0 platform/host contracts; planned. |
| P2 | Responsive multiple persistent sessions and recovery | P1; planned. |
| P3 | Phone-owned four-provider agent with selectable approval | P0 provider contracts and P2; planned. |
| P4 | iCloud app-data sync and cross-device recovery | P0 sync contract plus P2/P3; planned. |
| P5 | Combined usable native iPhone/iPad journeys | P1–P4; planned. |
| P6 | Signed TestFlight build and App Store preparation | P5 and signing/service prerequisites; planned. |

Tasks, actual evidence requirements and exit challenges are in [the phase plan](phases/mvp.md). No phase is delivered merely because its plan is saved.

## Resume

The checkout contains the upstream workflow bundle and these initial local discovery records. No application code has been created. Connectivity and credential sync for the first release are confirmed. The [MVP gap draft](specs/mvp-gap-proposals.md) now proposes the remaining terminal/baseline, responsiveness, prepared-host, recovery/history, agent-control and cross-device/account contracts. Await the user's decisions by numbered group/clause, then reconcile the foundation, architecture and phase plan and recheck affected claims. Native/host/provider research proceeds independently; actual implementation tests are not a prerequisite merely to know the desired behaviour. Product answers have not been inferred from silence. Technical responsibility is delegated; the human's time should be spent on product decisions rather than selecting architecture patterns or build tools.

## Provisioning work carried into the eventual delivery plan

EXEC-02 must close with actual repository scripts and cloud-init configuration, supported-host documentation, and an end-to-end connection/readiness check. Plan safe repeat execution and verify required baseline commands on a provisioned test host. A YAML parse or script syntax check alone cannot establish server readiness. These are required planned deliverables, not implemented provisioning.

## Early follow-up release: in-app cloud provisioning

**Target:** Version 1.1 or 1.2, exact placement pending.
**Requirement:** [CLOUD-01](specs/product-foundation.md#cloud-01-in-app-provisioning-in-an-early-follow-up-release).
**Status:** Planned product scope; delivery planning remains incomplete.

- Define supported cloud providers, account ownership, provisioning actions, connection handoff, failure recovery, and cost visibility.
- Reuse the MVP baseline configuration/provisioning boundary rather than creating a separate incompatible environment definition.
- Plan and verify an in-app journey that provisions the agreed baseline and connects the interactive terminal to it; distinguish test-provider evidence from live provider checks.

This is an early product milestone, not an indefinitely deferred possibility. Its open choices do not block independent MVP discovery. No cloud credentials, provider integration, or provisioning operation has been configured or executed.

## Session continuity work carried into the eventual delivery plan

SESSION-01 requires a remote shell/session lifetime independent of the iOS process, durable client session identity, reconnect/reattach behaviour, and prevention of automatic duplicate command execution after ambiguous disconnects. This does not assign agent orchestration to the host: AGENT-03 records the phone-runtime expectation and open pause/resume contract. Configure the baseline server's persistence capability. Verify against actual app termination/relaunch and interrupted transport with a live remote task; a transport reconnect or mocked session identifier alone is insufficient. For existing hosts, SETUP-01 requires the user-run compatibility script and in-app instructions. Define capability-check failures and host-failure behaviour before claiming continuity across arbitrary SSH hosts.

## Follow-up convenience: setup an existing host from the app

[SETUP-02](specs/product-foundation.md#setup-02-optional-later-automatic-setup-through-ssh) records the desired ability to run the same compatibility/setup mechanism through authenticated SSH. This is deferred from MVP, with exact release unassigned. It is distinct from creating/managing a cloud environment in CLOUD-01. Preserve a reusable setup boundary now; do not build or claim automatic remote setup during this planning stage.

## AI integration and model routing

- **MVP:** [AI-01](specs/product-foundation.md#ai-01-bring-your-own-model-credentials-for-mvp), user-supplied provider credentials. Define and validate the first supported model/tool-call journey and provider error recovery.
- **Feasibility investigation:** [INTEGRATION-01](specs/product-foundation.md#integration-01-assess-warp-account-feasibility). Assess supported authentication/API access, account requirements, mobile portability and source-reuse/license obligations. This is not a promised working integration or an MVP AI prerequisite.
- **Later capability:** [MODEL-01](specs/product-foundation.md#model-01-later-model-routing-and-switching), OpenRouter-inspired model switching/routing. Exact behaviour and release are unresolved; keep a provider boundary in the architecture and do not silently expand MVP scope.

The [initial Warp-account disposition](research/warp-account-feasibility.md) found official external cloud/factory run APIs and scoped API-key authentication. Account-backed phone inference/mobile sign-in remains unresolved; no live provider, Warp-account operation or native API build was performed.

## Current agent-runtime clarification

The user accepted a phone-owned coordinator for MVP, with persistent terminal command execution on the remote host. Continuing work should be a configurable default where execution is available; reliable new reasoning/dispatch after phone suspension/termination is not established. Define the observable pause/resume and recovery presentation, preserving already-running remote commands. Research newer continued-processing APIs before treating all background work as impossible. Keep the task/command approval setting separate from the background-continuation setting. Provider names have since been explicitly settled; validate their exact contracts independently. The [runtime proposal](design.md) gives the phone/remote division and recovery behaviour for product discussion, with Design in progress.

## Later research: cloud agent management

[AGENT-CLOUD-01](specs/product-foundation.md#agent-cloud-01-later-cloud-agent-management-research) is a later investigation into coordinating agent work independently of the phone while acting on terminal sessions. Evaluate value for mobile-terminal workflows, state/authority transfer and overlap with existing agent products. No release target or implementation commitment is assigned. Keep it separate from the version 1.1/1.2 cloud-provisioning milestone and from model routing.

## iCloud and distribution work carried into the delivery plan

SYNC-01 must close through actual two-device/account-specific CloudKit and iCloud Keychain evidence, including SSH/provider credential availability, updates/removal, metadata-first arrival, disabled/unavailable Keychain, offline reconciliation, account changes and prevention of execution from replicated history. Apple sync APIs do not supply an always-immediate schedule or agent-runner lock. Implement and verify execution ownership independently.

PLATFORM-01 requires usable iPhone and iPad flows plus a signed release artifact/TestFlight validation before App Store release. Native runtime feasibility and Expo/EAS service compatibility are assessed separately; no selected service has been authenticated or exercised. Apple developer/account/entitlement prerequisites are release/CloudKit dependencies, not secret values to request in chat.

## Planning review

A fresh read-only reviewer was assigned to derive obligations from the original user scope and inspect the saved specifications/design/phase plan. The independent reviewer identified seven planning gaps; the corrected tasks/check contract were re-inspected and all seven were resolved at the task/planned-evidence level. Corrections cover documentary handoff, check configuration, non-Linux host closure, stateful/interactive terminal-agent evidence, continuation/agent responsiveness, TestFlight ordering and bounded Warp feasibility. The draft is acceptable as work in progress. Credential-sync scope has since been explicitly confirmed; retention/recovery details, empirical feasibility and the full handoff remain unresolved. This is planning review, not runtime verification or authorization to publish.

## Understand readiness audit

A distinct review of the saved claims and current agreements found that the high-level MVP direction is well established, but the whole MVP is not yet Ready for Design. The [claim-level matrix](specs/product-foundation.md#readiness-review) now uses Open/Satisfied for named promises and concrete contrasting cases, with future scope, documented feasibility, hypothetical examples and implementation validation kept distinct. All 23 requirement references and domain terms are covered; Open outcomes remain visible rather than being cleared by the earlier successful planning review. Next resolve a focused recovery/data/control round and draft terminal/performance acceptance under the delegated engineering role.
