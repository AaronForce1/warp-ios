# Warp iOS MVP delivery plan — draft

**Planning status:** Planning in progress. Core product direction and iCloud Keychain credential sync are agreed; raw terminal retention, some recovery/data details and material native/host feasibility remain unresolved.
**Delivery:** Planned. No application, host helper, cloud-init template or release has been implemented.
**Owner:** Codex owns engineering design, decomposition, verification planning and record updates. The human confirms product scope. Local discovery/planning is authorized; this plan does not authorize publication, external-host changes or release.
**Inputs:** [Product foundation](../specs/product-foundation.md), [runtime design](../design.md), [preferences](../PREFERENCES.md), [research](../research/native-stack-and-sync.md), and the bundled [verification policy](../../.claude/skills/_shared/verification-policy.md).

One coordinator should own shared contracts and the roadmap. Tasks below are sequential by default; no parallel workers or worktrees are created by this plan. Each phase includes integration, source/design comparison and evidence updates, not only isolated implementation work.

## P0 — Resolve executable platform and contract feasibility

**Outcome:** a scoped, reproducible native/host/provider contract that can support the first user journey. Read-only candidate/contract research and requirements/design reconciliation are authorized now. Prototype application/host implementation and service operations are planned execution tasks, not implicitly authorized by the planning grant; they require the later implementation scope, platform capability and any specific external access.

| Task | Closing work and requirements | Prerequisites | Planned evidence |
|---|---|---|---|
| P0.1 | Select and pin Swift/Xcode/deployment target, native terminal/SSH candidates and release tooling; assess supporting UI/analysis skills and applicable verification tools. Supports PLATFORM-01, TERM-01, SSH-02. | Documented native direction. macOS/Xcode needed for actual builds. | iPhone/iPad terminal PTY prototype build, password/key connection, interactive input/output/resize and release-service compatibility result; source-level docs alone are insufficient. |
| P0.2 | Define prepared-host capability/identity/persistence protocol, durable command identities and execution ownership. Define selected-session working-directory/environment semantics, command completion/result boundaries and manual/agent input ownership; raw PTY bytes alone are not a completion protocol. Preserve host-OS-independent SSH scope; record Linux baseline and explicitly assessed macOS/Windows or other relevant SSH-host persistence compatibility. Supports SETUP-01, SESSION-01/02, SSH-01. | Accepted direct SSH and persistence requirements. | Prototype interrupted transport and host process/session observation; identify unsupported host capabilities without relabelling authentication as readiness. |
| P0.3 | Apply agreed CloudKit app-data plus iCloud Keychain credential sync; define raw terminal retention, recovery/takeover and no-iCloud/Keychain UX, one app-data sync/store owner and deletion/account policy. Supports SYNC-01, AGENT-03. | Outstanding product scope decisions. | Record schemas/state transitions and concrete conflict/account-change examples; later two-device checks remain required. |
| P0.4 | Pin a supported tool-using model/API contract for each agreed provider; define request/result/error boundaries and credential lifecycle. Supports AI-01, AGENT-01/02. | OpenAI, Anthropic, DeepSeek and Qwen scope. Authorized provider credentials needed for live checks, not for reading public contracts. | Four-provider compatibility evidence or a specific missing prerequisite; never claim OpenAI-style protocol shape proves tool behaviour for another provider. |
| P0.5 | Reconcile saved capability requirements, glossary, acceptance/recovery examples and material-claim readiness review; finish selected architecture views/interfaces and the plan closure review. | Product answers and applicable evidence from P0.1–P0.4. Can perform unaffected local documentation now. | Explicit scoped Understand/Design handoffs under actual agreement/delegation; no unchecked material claim or scope change hidden as an implementation detail. Record what can start versus what remains blocked. |
| P0.6 | Configure the [project check contract](../conventions.md): native build/behaviour checks, host validation, architecture analysis/inspection and applicable quality tools. Pin tools/config, test representative required rules and document actual coverage/exclusions. | Selected languages/source layout, available platform and supported tool scope; installation/configuration belongs to later authorized execution. | Versioned executable commands/config plus evidence they fail for a representative violation and pass a corresponding allowed case; unavailable required tooling remains a blocker or recorded authorized exception. |
| P0.7 | Complete bounded read-only Warp-account feasibility research: supported external authentication/API access, mobile portability, account prerequisites and source/license obligations. Supports INTEGRATION-01 without making it an MVP dependency. | Public documentation/maintained source available under current research authority; no live login or token extraction implied. | A linked disposition report: feasible for a named supported contract, infeasible under an established constraint, or unresolved with exact evidence/access needed. Existing desktop client code alone does not close supported mobile access. |

**Exit counterexample:** all documentation can look compatible while the SSH library cannot parse the user's key or the terminal cannot resize an interactive session. P0.1 must exercise those real boundaries before selecting a working stack. Missing macOS/provider/host capability remains a visible prerequisite; it is not a passing design experiment.

## P1 — Prepare a host and open the first native terminal

**Outcome:** a user follows repository instructions, prepares a baseline host, and uses the native app to connect directly and run a command.
**Prerequisites:** P0.1/P0.2 contracts, the scoped P0.5 requirements/design handoff and applicable P0.6 check configuration; an implementation grant and native build/test environment.

- **P1.1:** implement a repeatable existing-host compatibility/bootstrap mechanism and cloud-init configuration for the agreed Debian/Ubuntu baseline. Install/configure persistence capability and validate readiness; preserve existing host/user configuration. Link SETUP-01 and EXEC-02.
- **P1.1b:** implement/document platform-appropriate preparation and persistence for relevant non-Linux SSH hosts covered by the host matrix (including direct macOS/Windows cases), or record a concrete inability for product resolution before claiming host-OS-independent completion. Verify password/key interactive attachment and detached-session recovery on each supported path. A generic SSH client or actionable rejection of every non-Linux host does not close SSH-01.
- **P1.2:** build native iPhone/iPad host onboarding, setup guidance, password/key credential access and host-trust handling. Reject unsupported required SSH modes with a meaningful result. Link PLATFORM-01 and SSH-02.
- **P1.3:** attach a PTY to the native terminal, stream output/input and support resizing, disconnect/error states and explicit session identity. Link TERM-01, EXEC-01 and SSH-01.
- **P1.4:** integrate app and host, run the first complete journey and compare source responsibilities/dependencies with the agreed design. Update documentation with actual commands and supported-host evidence.

**Evidence:** actual fresh-host provisioning, safe repeat setup, connection from the app, a representative command and failing credential/missing-helper cases. Native compiler/build, focused protocol checks and native UI journeys apply. Scripts/YAML lint and a successful TCP/SSH handshake cannot replace this end-to-end result.
**Exit counterexample:** setup exits successfully but installs no working persistence mechanism. P1.4 must invoke the app's readiness/attachment contract, not merely inspect package presence.

## P2 — Persistent multi-session terminal and responsiveness

**Outcome:** multiple named sessions across saved hosts support useful interactive work and survive app termination/relaunch without duplicate commands.
**Prerequisites:** P1 integrated connection and host capability.

- **P2.1:** implement stable session identities, named host/session navigation and durable device session state. Switching visible sessions must not terminate other remote work. Link SESSION-02.
- **P2.2:** implement reconnect/reattach and ambiguous command-result reconciliation. Distinguish client loss from host-session loss, and explicit termination from detachment. Link SESSION-01.
- **P2.3:** validate desktop-like terminal scenarios: shell pipelines/redirection, control keys/signals, a fullscreen editor/process viewer, large output, paste/selection, resize and hardware keyboard interaction. Define representative shell/package/kubectl workloads on prepared hosts. For kubectl, exercise a declared test context, an authenticated read such as listing test resources, a controlled credential-helper/interactive-input case and a refused/expired credential result. SSH MFA remains excluded; a remote command's own interactive authentication is a distinct terminal case. Do not equate displaying kubectl help with a working cluster workflow. Link TERM-01/03/04.
- **P2.4:** measure local input/rendering latency, sustained output handling, attach/startup/reconnect and command runtimes separately under declared host/network/device conditions. Propose measurable acceptance thresholds from evidence rather than inventing an unmeasured speedup. Link PERF-01.
- **P2.5:** run combined interruption and multi-session journeys; reconcile source/design views and record evidence/limits.

**Evidence:** terminate/relaunch the actual app with a remote foreground job and changed working directory, reconnect to the same work, switch across hosts, and deliberately lose a completion acknowledgement. Report tested devices/workloads/network conditions; do not infer universal parity from a prompt rendering.
**Exit counterexample:** reconnect succeeds but repeats a side-effecting command. P2.2/2.5 must verify remote outcome identity and that recovery does not resend automatically.

## P3 — Phone-owned BYOK agent over the terminal

**Outcome:** typed natural language drives a multi-step terminal task from the phone, with the user's selected approval mode and visible command/results.
**Prerequisites:** P0.4 provider contracts and P2 execution/recovery boundary; credential storage contract from P0.3 for any sync-related portion.

- **P3.1:** implement native provider settings, protected credential lifecycle and adapters for the four launch providers, with useful invalid-key/rate-limit/network recovery. Link AI-01.
- **P3.2:** implement phone conversation/task coordination, approval policy, terminal tools and task checkpoints. Both per-command and task approval must affect dispatch. Treat host output/model suggestions as data, not authority. Link AGENT-01/02/03.
- **P3.3:** define and implement manual-versus-agent session ownership, user interruption/cancellation and phone background/pause/resume behaviour. The continuation preference defaults on as requested, is user-configurable, and has a defined persistence/sync and next-dispatch contract. Verify both settings: off stops starting new steps when backgrounded; on attempts eligible continuation while iOS grants runtime. Neither stops an already-running remote command solely because UI visibility changes, nor promises execution after suspension/termination. Investigate applicable continued-processing APIs. Link AGENT-03, SYNC-01 and SESSION-01.
- **P3.4:** integrate and verify task success, declined command, cancellation, provider failure and ambiguous disconnect with a real terminal boundary. Include a stateful multi-step task whose working directory/environment persists, incomplete output, a fullscreen/interactive program, a host command requiring interactive input, and manual takeover. Do not send a second command into a still-running program or execute it in an unrelated default-directory SSH channel. Record observed code responsibilities and required review evidence.
- **P3.5:** measure agent UI/approval responsiveness and model/provider response versus terminal dispatch/command latency separately under declared device/network/provider conditions. Verify setting states and restore of task progress after suspension/termination without replay. Link PERF-01 and AGENT-03; fast terminal rendering alone cannot close agent responsiveness.

**Evidence:** a real terminal task and controlled provider responses for repeatable failure/policy cases, plus separate authorized live compatibility checks for each provider. Mocked provider UI alone does not establish command execution or live model compatibility.
**Exit counterexample:** every approval UI test passes but another code path dispatches a declined command. P3.2/3.4 must observe the execution boundary. Provider/key failures must not break the already-working manual terminal.

## P4 — MVP iCloud sync and cross-device recovery

**Outcome:** the agreed host/preferences/session/conversation records and Keychain credentials converge across an iPhone and iPad, enabling authenticated use without duplicate execution or account-data mixing.
**Prerequisites:** P0.3 sync/credential scope and ownership contract, P2 session state and P3 conversation/agent state.

- **P4.1:** implement one local-replica/CloudKit sync adapter with stable record identifiers, version/conflict policy, tombstones and visible pending/error status. Link SYNC-01.
- **P4.2:** implement account-change/sign-out/unavailable-iCloud handling, retention/deletion behaviour, and the agreed iCloud Keychain credential-sync policy for SSH passwords/private keys and provider API keys, linked by stable identifiers. Test update/removal, unsupported/unavailable sync and metadata-first arrival without unrelated-credential fallback. Link SYNC-01 and AI-01.
- **P4.3:** reconcile a second device discovering a persistent session and any explicit coordinator takeover through the host ownership contract. Synced history must not dispatch commands. Link SESSION-02 and AGENT-03.
- **P4.4:** exercise actual two-device CloudKit and Keychain sync, authenticated SSH/provider use from synchronized credentials, concurrent/offline edits, credential update/removal, metadata/credential arrival ordering, disabled Keychain, account transitions and app relaunch; compare source sync/execution dependencies with the design.

**Evidence:** native Apple developer/iCloud test setup and two-device/account-specific checks. A serialized record or local mock sync does not close cross-device acceptance. Do not promise instant propagation or use CloudKit metadata as the only runner lock.
**Exit counterexample:** data appears on the iPad, but restoring the conversation re-executes an old tool call. P4.3/4.4 must observe that replication alone performs no remote action. A stale ownership record must not permit a second active dispatcher.

## P5 — Integrated iPhone/iPad product acceptance

**Outcome:** the manual/agent/session/sync flows form a usable native app on both launch form factors.
**Prerequisites:** P1–P4 integrated evidence; earlier phase failures stay visible.

- **P5.1:** reconcile native session and agent navigation, onboarding, loading/empty/error/recovery states, text selection/paste/control-key input, hardware keyboard and accessibility across both devices. Link PLATFORM-01 and TERM-01.
- **P5.2:** run the combined journey from user-supplied-host preparation through direct terminal work, agent approval, interruption/relaunch and second-device sync. Recheck representative responsiveness and regressions affected by integration. Link the corresponding phase evidence.
- **P5.3:** apply required configured compiler/build/quality checks, review the actual patch against requirements and design, derive observed architecture views and resolve findings. Update agreements only with applicable authority; missing checks are not waived by a favourable review.

**Evidence:** native UI journey evidence and concise screenshots/interaction traces, source-specific review and architecture comparison. Record agent inspection separately from human review. Confirm configured checks actually ran; no arbitrary test-count/coverage score replaces the outcome.
**Exit counterexample:** independent terminal and sync checks pass, but iPad navigation reconnects to the wrong host after synchronization. P5.2 must combine those boundaries rather than reusing isolated passes.

## P6 — TestFlight and App Store release preparation

**Outcome:** a reproducible signed iOS artifact is usable through TestFlight and has a concrete App Store submission handoff.
**Prerequisites:** P5 scoped acceptance and actual developer/account/signing/CloudKit configuration. Upload/publication requires a separate authorized external action.

- **P6.1:** validate the selected native archive workflow and EAS Build/Submit service compatibility. Pin actual tools/configuration; preserve a supported native build path if a service integration fails. Link PLATFORM-01.
- **P6.2:** prepare entitlements, account-scoped CloudKit production schema/migration, bundle/version/signing metadata and store-facing descriptions/privacy declarations for actual data flows. Do not put credential values in repository records.
- **P6.3:** produce and inspect the signed release artifact using the selected build pipeline. No upload or distributed acceptance is implied by an archive.
- **P6.4:** perform an authorized TestFlight upload and confirm processing/build availability. Prerequisite: P6.3 artifact plus actual upload authority/account setup.
- **P6.5:** exercise that distributed TestFlight build on both device types against the real sync/host contracts, including the production CloudKit schema and entitlements. Prerequisite: successful P6.4 processing; a build not uploaded cannot be a distributed-test result.
- **P6.6:** perform a separately authorized App Store submission, record observed review/publication outcomes, and reconcile release documentation/remaining limitations. Prerequisite: P6.5 acceptance plus actual submission authority. Review is an external outcome, not guaranteed by archive/upload success.

**Evidence:** archive/signing logs, distributed-build acceptance and observed TestFlight/App Store processing. A simulator Debug build cannot replace signed-distribution/production-CloudKit evidence.
**Exit counterexample:** development-device iCloud sync passes but the TestFlight build uses an uninitialized production schema. P6.2/P6.5 must test the distributed build's actual entitlements and production data path.

## Coverage review and current limitations

This is a planning draft under independent review. The first review pass identified and corrected missing documentary handoff work (P0.5), check configuration/evidence ownership (P0.6 and the check contract), non-Linux prepared-host closure (P1.1b), stateful/interactive agent execution evidence (P0.2/P3.4), configurable background/agent performance evidence (P3.3/P3.5), bounded Warp feasibility (P0.7), and upload-before-distributed-TestFlight-test ordering (P6.3–P6.6). A fresh independent recheck inspected the changed records and resolved all seven findings at the task/planned-evidence level. The draft remains Planning in progress: empirical feasibility, product sync details and the full documentary handoff are not thereby resolved. Requirements are mapped to closing work as follows:

| Obligation | Closing work | Required boundary and remaining limit |
|---|---|---|
| Interactive, responsive remote terminal and Linux baseline | P1.1–P1.4, P2.3–P2.5 | Native app plus prepared host and declared workloads; performance thresholds need evidence-based selection. |
| Direct password/key SSH with exclusions | P0.1, P1.2–P1.4 | Actual supported authentication/key and host-trust flows; no bastion/MFA/forwarding scope added. |
| Host preparation/cloud-init | P0.2, P1.1/P1.1b/P1.4 | Fresh/repeated provisioning and app readiness, not lint alone. Other-host persistence feasibility remains open. |
| Persistent multiple sessions without duplicate actions | P2.1/P2.2/P2.5 and P4.3/P4.4 | App termination/relaunch, remote work identity and cross-device dispatch ownership. |
| Phone-owned four-provider agent and approval modes | P0.4, P3.1–P3.5 | Actual execution-policy boundary plus separately identified live-provider evidence. |
| iCloud MVP sync | P0.3, P4.1–P4.4, P6.2/P6.5 | Two-device edits/account/ownership and distributed-build schema; Credential sync is agreed; raw terminal retention and unavailable-sync behaviour still need definition. |
| iPhone/iPad and App Store distribution | P0.1, P5.1–P5.3, P6.1–P6.6 | Native device journeys and authorized signed release; no current Xcode or service credentials validated. |
| Warp-account feasibility | P0.7 | Supported external access/mobile/source/license disposition; unresolved live access is explicit and does not block the independent BYOK implementation. |
| Documentation, conformance, review and integration | P0.5/P0.6, P1.4, P2.5, P3.4, P4.4, P5.3, P6.6 | Actual source snapshot, required check results and remaining evidence; publication is separate authority. |

Later voice, on-device Linux execution, model routing, automatic existing-host setup and cloud agent management remain distinct future scope. In-app cloud provisioning is assigned to version 1.1 or 1.2 and must reuse the baseline contract, but its provider/ownership plan is not yet complete. These deferrals do not remove any agreed MVP requirement.

**Next safe work:** define remaining retention/recovery details and complete P0.5 documentary requirements/design/plan reconciliation plus read-only P0.7 research. A bounded P0 prototype spike can become ready for its own later implementation grant while full application feasibility is still unknown; do not require prototype implementation under the current planning-only scope or present a spike as full-app readiness. P1 requires the relevant P0 empirical outcomes and scoped handoff. No permission to purchase/provision external infrastructure or upload an app is implied by this document.
