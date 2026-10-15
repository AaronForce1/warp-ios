# Warp iOS product foundation

**Understand status:** Clarification ongoing.
**Agreement:** A responsive interactive terminal with Debian/Ubuntu-like capabilities and an agentic overlay is the product target. On-device execution remains a long-term preference; requiring a connection to an external execution environment is explicitly accepted for the first release.
**Delivery:** No application source, Xcode project, Swift package, or application tests exist in this checkout. The AI workflow bundle is installed.
**Related records:** [Feature map](README.md), [glossary](../GLOSSARY.md), [roadmap](../ROADMAP.md), [Understand workflow](../../.claude/skills/understand/SKILL.md).

## Confirmed direction and authority

- Build the requirements and architecture for a new Warp iOS application from scratch.
- The agent owns technical investigation, architecture recommendations, documentation, and delivery planning.
- The human confirms product requirements and consequential product tradeoffs; routine engineering decisions are delegated.
- Use Understand, Design, and Plan Delivery for this scope. Apply Implement, Review Change, and Orchestrate Delivery at their relevant later stages, rather than treating their availability as completed work.
- Maintain repository records as discussion develops. The user's subsequent “Create PR” request authorizes committing and pushing this documentation on a branch and opening a pull request. Product proposals remain unconfirmed; merging, external-host changes and app releases are outside that request.

## Verified starting point

Repository inspection after updating from upstream found the workflow skill bundle and a product README, but no application implementation or build/test configuration. The companion desktop repository is available for targeted inspection; its existence does not prove an iOS-compatible backend contract or mobile integration.

## Problem, users and intended outcome

People using a terminal from an iPhone or iPad face the user's reported iSH performance problem, difficult mobile command entry, and lost work when mobile apps are suspended or terminated. The desired result is desktop-like interactive terminal capability and responsiveness, assisted by typed agent instructions, while preserving remote work and sharing app data/credentials across devices.

The MVP user supplies a reachable SSH host and model-provider credentials, prepares the host through repository instructions, and uses a native iPhone/iPad app. Developers/operators are a working audience inference from the terminal/kubectl examples, not a confirmed exclusive persona. The accepted capability scope does not depend on picking a job title; reference workflows and their priorities still need definition.

The accepted MVP executes shell commands remotely and coordinates the agent on the phone. A connected MVP is an agreed way to pursue the original local-terminal goal; local Linux execution remains a future goal. Source research supports scoped candidate approaches, not a universal claim that ARM architecture alone eliminates every performance or OS restriction.

## Scope and placement

MVP covers direct password/key SSH, repository-provided host preparation and cloud-init, interactive persistent multi-session terminals, phone-owned typed BYOK agent control with selectable approvals, iPhone/iPad distribution, and iCloud app-data plus Keychain credential sync. The requirements below own the exact agreements and remaining boundaries.

Bastions, SSH MFA and port forwarding are explicitly excluded from MVP. Voice, local Linux execution, automatic SSH host preparation, model routing and cloud agent management are later work or research, with their documented evidence/placement limits. In-app cloud provisioning is planned for version 1.1 or 1.2. Detailed future-provider/hosting decisions do not block closing the bounded MVP requirements.

## Confirmed product requirements

### TERM-01: Native interactive terminal

A full interactive terminal is core to the product, not merely an agent dashboard. Users must be able to type commands and interact with their output. iTerm on macOS is the experience reference; an exhaustive compatibility guarantee has not been defined or verified.

### TERM-02: On-device execution within iOS constraints

On-device execution is the preferred experience, with performance sufficient to avoid the user's reported unacceptable iSH slowness. Avoid slow x86 emulation as the default foundation. The user permits investigating an iOS client backed by a terminal environment on their computer or a cloud server, although this is less ideal than local execution. The user subsequently confirmed that requiring a connection is acceptable for the first release. Offline execution of the full Linux baseline is therefore not a first-release prerequisite; this does not imply it has been abandoned as a longer-term goal. Work must respect iOS sandboxing; root-level control of the iPhone is not requested. ARM compatibility alone does not establish unrestricted executable loading or desktop process semantics.

### TERM-03: Remote and infrastructure workflows

SSH and kubectl workflows are explicitly requested. For the accepted connected MVP, terminal commands including kubectl execute in the remote host environment. The phone owns terminal interaction and agent coordination. On-device Linux command execution is a longer-term goal, not an unresolved MVP prerequisite. Define and verify host credential-helper/interactive authentication behaviour for the agreed workflows.

### AGENT-01: Agentic layer over terminal execution

The intended direction is for users to converse with an agent that carries out terminal operations, while retaining direct command input. Warp companion and agent capabilities are part of the product direction. Typed natural-language instructions should be translated into terminal operations. A voice interface is an intended later capability; its launch timing is not fixed. MVP model access and user-selectable execution approval are defined below. Warp-account integration remains a separate feasibility investigation; voice and other later capability details remain to be planned.

### AGENT-02: User-selectable execution approval

The user must be able to choose between approving an overall task and allowing its steps to execute, or approving individual commands before they run. Neither mode is imposed as the only available experience. The selected mode must govern agent-initiated execution, rather than being a cosmetic preference.

Acceptance examples:

- In command-approval mode, a proposed command waits for approval; declining it does not execute it.
- In task-approval mode, approving a bounded task permits its steps without requiring routine per-command approval, subject to the task's agreed authority and boundaries.

The default mode, preference scope and persistence, when mode changes take effect, task boundaries, rejection/cancellation behaviour, and any exceptional operations need definition. This is a product control requirement, not authorization for this planning agent to execute commands on the user's external hosts.

### AI-01: Bring-your-own model credentials for MVP

MVP AI access uses model-provider credentials supplied by the user. A Warp account is not a prerequisite for this access path. Launch provider scope is OpenAI, Anthropic, DeepSeek, and Qwen (Alibaba), with no additional must-have providers identified. Exact model IDs, supported provider endpoints/tool-call contracts, credential onboarding/replacement/removal, request execution location, and error behaviour remain to be defined. Support must be validated per provider rather than inferred from nominal API compatibility. This requirement does not authorize collecting credential values in chat or exposing them in repository files/logs.

Acceptance direction: after configuring credentials for a supported provider, the user can perform the agreed agent terminal journey; missing, invalid, rate-limited, or revoked credentials produce a clear recoverable outcome. A working terminal must not be mistaken for proof that the model's tool execution works. Exact provider-specific contracts have not been tested.

### INTEGRATION-01: Assess Warp-account feasibility

Investigate whether supported Warp authentication and agent/service interfaces can integrate into this iOS application. The user considers this desirable, but it is not the MVP AI dependency. The feasibility result must distinguish documented supported access, observed source implementation, mobile portability, required account/entitlements, and unverified assumptions. Source availability or desktop login does not prove permission or compatibility for third-party mobile integration. The [initial feasibility disposition](../research/warp-account-feasibility.md) found official cloud/factory-run APIs; account-backed phone inference and a mobile sign-in contract remain separate unresolved capabilities.

### MODEL-01: Later model routing and switching

The later product direction includes routing or pivoting between models in a manner inspired by OpenRouter. Whether this means using OpenRouter directly, implementing custom routing, manual model changes, automatic fallback, or task-based selection is unresolved. No exact release is assigned. The MVP design should preserve a provider boundary without implementing unagreed routing policy or promising interchangeable tool-call semantics.

### AGENT-03: Phone-owned agent coordination

The user expects the agent to run on the phone rather than assuming a remotely hosted agent. The candidate interpretation is that the iOS app owns conversation state, model requests, tool planning, approval policy, and SSH dispatch; configured model providers perform inference, and the remote host runs terminal commands. Fully local on-device model inference has not been requested or established by the BYOK requirement. The user has accepted the phone-coordinator/remote-terminal division for MVP. See the [runtime architecture direction](../design.md). The model inference remains at the selected BYOK provider; on-device model inference is not established.

The user also requested that continuing agent work while disconnected be enabled by default and configurable. This preference was stated before identifying the phone-versus-host runtime distinction. Preserve that preference, but do not silently convert it into permission to move the agent to the host or promise execution after iOS terminates its process.

**Runtime consequence to retain in acceptance:** a phone coordinator can continue only while iOS grants execution time. Long-running commands already dispatched to a persistent remote session can survive independently. Phone-owned coordination is accepted; requirements and recovery UX must explicitly reflect that new agent decisions pause when iOS suspends/terminates the coordinator, and that persisted state supports resuming later. This physical execution limit does not waive the requirement to preserve already-dispatched remote work. The exact continuation-setting semantics and recovery presentation remain to be defined. The agent's durable state and remote command reconciliation must avoid duplicate actions after restart. No server-side agent has been approved as the default.

### AGENT-CLOUD-01: Later cloud agent management research

Investigate optional cloud-hosted agent management that can continue coordinating actions against terminal execution independently of the phone. This is future research, not an approved MVP remote agent or an assigned release commitment. Evaluate the benefit for this mobile terminal product, ownership/credential handoff, recovery and authority, and overlap with existing cloud coding-agent products. Avoid assuming the app must grow a general-purpose hosted agent platform to meet the MVP.

This investigation is separate from in-app provisioning (CLOUD-01, version 1.1 or 1.2), automatically preparing an existing host (SETUP-02), and later model routing (MODEL-01).

### TERM-04: General Linux environment baseline

The user wants at least the capabilities of a minimal Debian or Ubuntu installation, using a pulled distribution container image as the reference. A hand-picked collection of familiar command names is not an equivalent product outcome. The precise baseline distribution/release, package installation behaviour, shell compatibility, interactive applications, and workload matrix must be made testable. The Docker image reference does not by itself establish a requirement to run a Docker daemon on the iPhone.

### EXEC-01: Connected execution is acceptable for the first release

The first release may require network connectivity to a real Linux execution environment. The terminal UI and agent controls live in the iOS application; commands may execute on a personal-computer or cloud backend. This explicitly permits a remote backend without treating a dashboard as an interactive terminal. Bring-your-own host and repository-provided setup/cloud-init are agreed for MVP; in-app cloud provisioning is planned for version 1.1 or 1.2.

### EXEC-02: Bring an existing host, with repository-provided scaffolding

For the MVP, the user supplies an existing server or computer. The repository must also provide scripts to scaffold a baseline execution server, including cloud-init configuration for easy provisioning. Managed cloud-environment creation inside the application is deferred from the MVP and explicitly planned for version 1.1 or 1.2; the exact release is not decided. The user subsequently clarified that SSH compatibility, rather than host OS, defines connection scope. Direct macOS/Windows or other host shells are in scope when reachable through supported SSH interaction; the application does not supply missing host commands or turn every connected OS into Linux.

The desired onboarding result is a reachable baseline environment ready for the terminal client, not merely a script exiting successfully. Supported OS versions, connection setup, installation privilege requirements, and the application-to-host readiness check still need design and acceptance definition. No live provisioning has been requested or performed.

### SETUP-01: Explicit bring-your-own-server preparation

For an existing host, the user runs the compatibility/setup script maintained in this repository. The MVP application provides prerequisite/setup instructions as part of bring-your-own-server onboarding. Cloud-init provisions the same intended baseline for a new server; the existing-host script prepares or diagnoses a supplied host. Host preparation is not assumed merely because SSH credentials authenticate successfully.

The intended result is a host compatible with the app, including the session-persistence capability required by SESSION-01. A compatibility/readiness check must report whether the app's required capabilities are present and give actionable setup guidance when they are missing. Exact supported platforms, privileged steps, and check implementation belong to Design; SSH connection scope must remain distinguished from verified prepared-host capabilities.

Acceptance direction: given an unprepared existing host, onboarding explains the required repository script; after successful setup and readiness verification, the user can establish an interactive persistent session. If preparation is incomplete, the app explains the missing prerequisite rather than silently promising session continuity. Concrete commands and live provisioning validation do not yet exist.

### SETUP-02: Optional later automatic setup through SSH

The desired later experience is that the app can authenticate using valid user-supplied SSH credentials and run the same setup mechanism remotely. This is not required for the MVP, and no exact follow-up release is assigned. Do not conflate it with CLOUD-01, whose in-app cloud provisioning target is explicitly version 1.1 or 1.2. Remote setup may require capabilities beyond successful authentication; its privilege/interaction and failure behaviour must be defined before delivery.

### SSH-01: Host-OS-independent SSH connections

The MVP connects to SSH-compatible hosts without restricting the product to Debian or Ubuntu servers. The remote host supplies its shell, programs, filesystem, and operating-system semantics. The Debian/Ubuntu baseline applies to the repository's scaffolded environment, not to a promise that every SSH host supports the same commands.

“SSH-compatible” remains a product direction, not a claim that every SSH protocol mode, authentication method, algorithm, forwarding extension, or server policy is supported. Define the interactive session contract and representative compatibility evidence. An SSH server providing only file transfer or disallowing interactive sessions cannot be counted as an interactive terminal merely because authentication succeeds; the app's expected outcome for such a host remains to be defined.

### SSH-02: Direct password/key authentication; advanced SSH features deferred

MVP SSH authentication supports passwords and SSH keys. Bastion/jump hosts, SSH MFA, and port forwarding are explicitly outside the MVP. This narrows the client feature set while retaining host-OS-independent direct connections. Servers requiring an excluded connection/authentication flow are not promised as MVP-compatible.

Acceptance direction: connect directly to a prepared host using password or a supported SSH key, establish an interactive terminal, and recover its persistent session. Authentication rejection or an unsupported required mechanism must yield an actionable result without claiming a working shell. Exact key formats, passphrase handling, and host-key verification are technical contracts to define and validate.

### PLATFORM-01: iPhone and iPad, with App Store distribution

Both iPhone and iPad are launch targets. App Store distribution is the intended release path, with TestFlight as a proposed validation/distribution step. Native components are the user's preference. The user liked Expo as middleware supporting distribution; this is a preference to investigate, not a mandate to put the app runtime in Expo or React Native.

Acceptance direction: the terminal and agent flows are usable on each device form factor, with appropriate touch/keyboard interaction and layout. A signed build and App Store Connect/TestFlight processing must be evidenced during release preparation; publication requires an authorized release operation and the relevant account setup. No app has been built, signed, uploaded, reviewed, or published.

### SYNC-01: iCloud synchronization in MVP

Cross-device synchronization through iCloud is required in MVP. Local-only persistence with synchronization deferred is not the agreed launch scope. A local replica remains necessary for reliable device state and use when iCloud is temporarily unavailable; local persistence does not replace the synchronization obligation.

The agreed synced dataset includes saved host profiles, app preferences, persistent session identities, and agent conversations/history. The user explicitly confirmed that SSH passwords/private keys and model-provider API keys also synchronize through iCloud Keychain in MVP. App data uses CloudKit; credential values use synchronizable Keychain items, with stable identifiers connecting credentials to their host/provider records. Raw terminal scrollback scope/retention needs definition and must not be confused with preserving the remote process itself.

Acceptance direction: two devices on the same iCloud account receive the agreed app records; changes propagate without duplicating hosts/sessions or replaying commands. Offline edits and deletions reconcile predictably. iCloud sign-out/account changes, quota/errors, and delayed sync must not mix users' data or trigger tool execution. Syncing records is distinct from transferring a live SSH connection or granting two devices simultaneous agent ownership.

Credential-sync acceptance examples:

- Given an iPhone with saved SSH credentials and provider keys, an iPad on the same user account with iCloud Keychain enabled can resolve the synchronized credentials and use the corresponding host/provider flows without re-entering their values.
- If host/provider metadata arrives before its Keychain item, the app shows that credentials are unavailable or awaiting sync; it does not report a credential-complete state or use an unrelated credential.
- Changes/removal of a synchronizable credential reconcile across linked devices, with eventual propagation stated honestly. Deleting an app credential does not itself revoke the external provider key or change the server password.
- With iCloud Keychain unavailable/disabled or an account transition, the app separates app-data and credential-sync state and protects the account boundary. Cross-device readiness must not be inferred solely from CloudKit metadata.


### SESSION-01: Preserve work across mobile interruption and relaunch

The MVP must preserve the remote shell session and already-running remote commands when the phone locks, the user switches applications, connectivity drops, or the iOS app is terminated and later relaunched. This preservation is distinct from an agent making new decisions after the phone app stops executing; AGENT-03 records the user's newly clarified phone-runtime expectation and the remaining continuation question. After connection is restored, the app must reattach to the same existing session rather than silently creating a new shell or replaying a previously submitted command.

The user suggested GNU Screen as a possible mechanism; that is a design suggestion, not a requirement to use a particular utility. Server-side session management and durable client session identity are candidate implementation responsibilities. Basic SSH connectivity alone does not establish this guarantee on every server.

Acceptance examples:

- Given an interactive session with a running foreground task and changed working directory, when the app is terminated and relaunched while the host session remains alive, reconnecting returns to that task/session rather than starting from a fresh shell.
- Given a side-effecting command submitted before the connection drops, reconnecting must not automatically rerun the command merely because its completion response was missed.
- Given a host without the required persistence capability, authentication success alone must not be reported as a verified durable-session experience. The user has now confirmed that existing hosts are prepared through the repository script and that the MVP app supplies setup instructions. No host should be counted ready without its required capabilities.

Multiple named sessions across saved hosts are confirmed in SESSION-02. Recovering work after remote-host reboot/process failure, exact retained output/history, explicit session deletion, and retention policies still require definition. Do not imply that keeping a multiplexer alive saves all application work after a host reboot.

### SESSION-02: Multiple named sessions across saved hosts

The MVP must support multiple named persistent terminal sessions across saved hosts. Switching the visible session must not interrupt work running in the others. This was explicitly confirmed in the final voice-session response.

Acceptance examples:

- Given named sessions on two saved hosts, switching from the first to the second leaves the first session's remote task running.
- After app termination/relaunch, saved host/session identities remain available and reconnect to the intended existing sessions, rather than attaching to the wrong host or silently replacing them.

The number of concurrently attached transports, agent-task concurrency, and terminal/history retention are separate decisions. Multi-device synchronization via iCloud is now an explicit MVP requirement in SYNC-01, rather than an inference from multiple saved sessions. Session caps must not be invented as product limits.

### CLOUD-01: In-app provisioning in an early follow-up release

The product roadmap must include managing cloud provisioning inside the iOS application in version 1.1 or 1.2. This is committed roadmap scope, not an excluded or merely optional idea. The exact release, providers, authentication/ownership model, supported operations, and cost/billing experience remain unresolved.

MVP scaffolding should provide a reusable baseline configuration so the later provisioning flow can produce the same agreed execution environment. Avoid assuming this requires a paid managed hosting service: user-owned provider accounts versus product-managed infrastructure is still a product decision. Future-compatible boundaries do not justify building the full cloud control plane during the MVP.

### PERF-01: Responsiveness is a core acceptance requirement

The user reports that iSH's execution speed is unacceptable and identifies this as the central terminal problem to solve. This is a product experience report, not a measured benchmark or proof that all of iSH's slowness comes from instruction emulation. Assess input/display latency, startup, command execution, sustained output, and agent responsiveness separately. For a remote architecture include network conditions and reconnection; do not promise every workload is faster because it executes remotely. Numeric targets and representative workloads are still open.

## Acceptance examples to complete

- In the connected MVP, a user types a command into an attached remote terminal, receives its output, and can continue interacting. The remote shell owns command semantics; terminal compatibility and interactive-program acceptance remain to be made concrete.
- A user connects to a chosen SSH host with the agreed direct password/key authentication and interacts with that remote session. Detailed disconnect/recovery and terminal compatibility acceptance are proposed in the gap draft.
- A user requests an operation conversationally and the phone-owned coordinator executes work in the remote terminal. Detailed command/result visibility, task boundaries and cancellation behaviour are proposed in the gap draft; selectable approval modes and runtime placement are already agreed.

These examples anchor discovery; they are not yet complete acceptance contracts.

## Remaining product acceptance gaps

1. **Terminal parity and baseline:** make desktop-like interaction and the Debian/Ubuntu reference concrete. Define representative fullscreen/control-key/shell/package/kubectl scenarios and supported-host outcomes; avoid promising every desktop capability through an undefined label.
2. **Performance:** agree what responsiveness means for those journeys under stated device/host/network conditions. The agent owns instrumentation and budget proposals; the user should not choose rendering libraries or invent latency numbers.
3. **Recovery and history:** settle host-reboot/process-loss outcomes, terminal output retention/sync/deletion, and the difference between preserving a shell, its output and an agent conversation.
4. **Agent control and data:** specify bounded task approval, exceptional elevated/destructive actions, model-context disclosure, manual takeover, cancellation, task concurrency, and what the user observes when phone coordination pauses/resumes. Phone-owned coordination and the available continuation setting are already agreed.
5. **Cross-device/account behaviour:** define who controls an active session/agent on two devices, and the user experience when iCloud or Keychain is unavailable, disabled, signed out or changed. Record replication cannot by itself settle active execution ownership.

These are unresolved observable outcomes. Existing approval modes, provider names, SSH exclusions, device targets, iCloud credential scope and the remote MVP boundary are not reopened.

## Proposed gap requirements for confirmation

The user requested initial MVP requirements for these gaps. The [numbered acceptance draft](mvp-gap-proposals.md) proposes observable rules and concrete acceptance examples:

| Gap | Proposed clauses | Agreement |
|---|---|---|
| Terminal parity, baseline and prepared-host boundary | [Group 1](mvp-gap-proposals.md#1-terminal-capabilities-and-host-baseline) | Proposed; not confirmed |
| Responsiveness and measurement conditions | [Group 2](mvp-gap-proposals.md#2-responsiveness-and-performance-targets) | Proposed; not confirmed or benchmarked |
| Client recovery, host loss, retained history and deletion | [Group 3](mvp-gap-proposals.md#3-recovery-history-and-deletion) | Proposed; not confirmed |
| Agent task/approval scope, Stop, takeover, continuation, AI context and exceptional actions | [Group 4](mvp-gap-proposals.md#4-agent-authority-and-lifecycle) | Proposed additions, including 4.6/4.7; existing selectable approval/runtime decisions retained |
| Device ownership, handoff, unavailable sync and account boundaries | [Group 5](mvp-gap-proposals.md#5-cross-device-control-and-icloud-availability) | Proposed additions; existing app-data/credential sync decision retained |

Confirmation can cover a group or a clause such as 3.3. The proposal's [saved-draft review](mvp-gap-proposals.md#proposal-review-and-confirmation) records its claims and counterexamples. The Open statuses below remain Open: a proposed target is not an agreed requirement or a measured result. Reconcile affected foundation/design/phase records after product decisions; technical feasibility evidence remains the agent's responsibility.

## Factual investigation and Design-owned choices

The agent owns the prepared-host capability/platform contract and evidence, provider/model/tool-call compatibility, native/Expo build/service compatibility, library versions, storage/schema/transport selection and performance instrumentation. Consequential claims of universal compatibility or guaranteed timing must be supported or narrowed; lack of an implemented app is not by itself a failure to understand desired behaviour.

Actual app/device/provider/SSH/iCloud tests belong to implementation validation unless a specific experiment is needed to establish a premise before committing to a scope promise. Do not require a working app merely to complete the Understand stage. Follow-up Warp/mobile-account possibilities remain scoped research; the documented cloud-run API is not a premise for MVP BYOK access.

## Latest product decisions and remaining sync detail

The latest answers establish these launch choices:

- Direct SSH with passwords and keys. Bastions, MFA and port forwarding are excluded from MVP.
- iPhone and iPad, with App Store distribution and a preference for native components; assess Expo for distribution tooling.
- iCloud synchronization is required in MVP.

The credential-sync question is answered: both app data and credentials synchronize in MVP, with SSH credentials/model-provider keys using iCloud Keychain. Saved host profiles, preferences, session identities and agent conversations are the agreed app-data scope. Raw terminal scrollback retention, account/unavailable-sync recovery and device takeover remain separate details to define.

Routine implementation choices remain delegated. Derive desktop-like terminal compatibility scenarios and representative performance workloads, define observable recovery/cancellation behaviour, and surface consequential product tradeoffs. Later research must not create new MVP requirements merely by being recorded.

## Design handoff questions

The agent owns stack selection, command-runtime adapters, terminal rendering, session boundaries, credential handling, and architecture. Implementation choices remain provisional while their consequential product behaviour is unresolved. A shared execution interface for direct and agent-initiated commands is a candidate, not an approved or implemented architecture.

## Readiness review

**Method:** distinct agent review of the saved claims, user decisions, domain terms, research limits and roadmap. The previous independent phase-plan review established task coverage, not Understand completion. Every status below concerns the named promise only; a future implementation is not represented as delivered or tested.

| Material claim and references | Evidence/decision and limits | Concrete challenge and result | Status |
|---|---|---|---|
| Problem and intended outcome: terminal, mobile input and work preservation | User-described iSH slowness/mobile-input difficulty and desired terminal plus agent. This is user experience evidence, not a benchmark. | A dashboard-only product would omit direct shell interaction and fail the stated goal. The agreed connected terminal plus agent retains that outcome. | Satisfied |
| TERM-01: “full interactive” desktop-like parity | Explicit user goal; SwiftTerm documents a native candidate, not exhaustive parity. | A prompt-only UI could pass a shell-command check while failing an editor, control keys or resize. The current spec has no complete accepted compatibility set. | Open — acceptance definition |
| TERM-02 / EXEC-01: connected MVP, local execution later | User explicitly accepted requiring a connection. iSH documents instruction emulation plus syscall translation; native terminal alternatives were examined. | A remote MVP would violate a mandatory offline promise, but the user explicitly permitted connected execution. Do not infer native ARM alone supplies a Linux environment. | Satisfied for release boundary |
| TERM-03: SSH/kubectl and remote infrastructure workflows | Explicit examples and accepted remote command boundary. | Displaying kubectl help does not establish authenticated cluster access or credential-helper interaction. P2.3 plans tests, but the representative expected workflow/error contract is not yet fully agreed. | Open — workflow acceptance |
| TERM-04: Debian/Ubuntu baseline | User's minimum-installation/container-image reference; Docker documents host-kernel dependence. | Extracting image files or supplying a handful of command names would not provide the requested Linux environment. Version/tool/permission/shell baseline remains undefined. | Open — baseline contract |
| EXEC-02 / SETUP-01: prepared existing host and repository/cloud-init setup | Explicit MVP setup direction; cloud-init documents first-boot provisioning. | Successful SSH login or a zero script exit can occur without durable terminal support. Required host capabilities, failure guidance and non-Linux preparation evidence need a bounded contract. | Open — capability/feasibility contract |
| SSH-01: host OS is not the connection restriction | Explicit “whatever is SSH compatible” direction, narrowed by SSH-02 and preparation. | A file-transfer-only server authenticates but has no interactive shell; a Windows SSH host may lack the selected persistence mechanism. Generic login is not enough to support the full host promise. | Open — interactive/prepared-host boundary |
| SSH-02: passwords/keys; excluded advanced flows | Explicit latest answer excludes bastions, SSH MFA and forwarding. | A required bastion route is outside the accepted MVP; it must not be counted as a promised direct-connect success. Key format/algorithm selection is a later contract, not permission to add bastions. | Satisfied for feature boundary |
| SESSION-01: remote work survives client interruption | Explicit user pain point and recovery requirement; tmux supports scoped detached-session behaviour. | App termination with a live host should reattach to existing work, while host reboot may destroy processes. The latter case and retained output are unspecified. | Open — recovery extent/history |
| SESSION-01: reconnect must not duplicate a submitted action | Derived acceptance correction consistent with preserving user work; source/test method remains pending. | A command may finish after its acknowledgement is lost. Blind replay can apply the side effect twice; the agreement requires reconcile-before-new-dispatch, not treating silence as proof of no execution. | Satisfied as desired recovery rule; validation later |
| SESSION-02: multiple named sessions across hosts | Explicit final voice confirmation. | Switching the visible session must not kill a different host's job or swap its identity. The existing examples define those outcomes; task concurrency is assessed separately. | Satisfied for named-session direction |
| AGENT-01: typed agent controls terminal work | Explicit product direction; phone/host roles clarified. | A chat reply suggesting a command without executing it would not meet the intended agent layer. Multi-step success, interactive input and task completion boundaries still need accepted examples. | Open — agent journey |
| AGENT-02: selectable task/per-command approval | Explicit “user should be able to choose.” | A preference toggle that still sends a declined command would fail. Both modes and no execution after rejection are specified. | Satisfied for selectable-mode requirement |
| AGENT-02: task boundaries, manual takeover and cancellation | The two modes are agreed; detailed lifecycle is not. | A manually started fullscreen app or a cancelled task could still receive a queued agent command. Approval of an overall task does not answer when control transfers or queued actions stop. | Open — observable control lifecycle |
| AGENT-02: exceptional elevated/destructive actions | The requirement leaves exceptional operations undefined; proposed clause 4.7 now describes a separate-confirmation default. | An ordinary task approval could be treated as permission for privilege escalation or deleting an entire environment. The proposed exception is unconfirmed and enforcement is unverified. | Open — exceptional authority contract |
| AGENT-01 / AI-01: model-context and credential disclosure | BYOK/provider scope is agreed; architecture states relevant context may be transmitted but leaves exact disclosure/redaction open. Proposed clause 4.6 defines boundaries. | Manual terminal use or unrelated sessions could otherwise be uploaded, while arbitrary secrets may evade detection. The draft limits automatic context and excludes stored credentials without a perfect-redaction claim. | Open — data disclosure contract |
| AGENT-03: phone coordinator, provider inference, remote shell | User accepted this MVP split; provider requests are distinct from local inference. | Moving coordination to the host would change the accepted runtime and credential path. Preserving remote command execution does not turn the provider into the phone's coordinator. | Satisfied for runtime ownership |
| AGENT-03: configurable continuation and pause/resume | Default-on where runtime is available was requested. Apple continued-processing and limited background APIs were examined, including contrary evidence to a blanket background prohibition. | Background permission can expire or the app can terminate. Existing work can survive remotely; new phone decisions cannot occur while its process is not executing. User-visible pause/resume and pending approval/command recovery remain incomplete. | Open — lifecycle acceptance |
| AI-01: BYOK and four named providers | Explicit provider list: OpenAI, Anthropic, DeepSeek and Qwen. No Warp account is required for MVP AI. | An API-key screen supporting only one provider would miss scope. Selection names are agreed; concrete supported tool-using model/API contracts remain Design/research work. | Satisfied for access/provider scope |
| AI-01: recoverable provider/credential errors | Desired error direction is documented; exact task-state result is not. | An invalid key, a rate limit or a provider response without usable tool output can follow successful SSH connection. Whether the task pauses/resumes/retries and what the user sees need acceptance definitions. | Open — failure outcome |
| PLATFORM-01: iPhone/iPad, App Store and native preference | Explicit latest answer; Expo native/EAS documentation provides scoped candidate evidence. | Native preference does not exclude Expo modules; an iPhone-only or simulator-only acceptance would miss the requested device/distribution scope. Build/service selection and actual signing belong to Design/delivery. | Satisfied for launch scope |
| SYNC-01: app data plus iCloud Keychain credentials | Explicit answer confirms both datasets/mechanisms; Apple documents native sync and Keychain constraints. | Host metadata can arrive before credentials. The specified outcome waits/reports unavailable credentials instead of assuming readiness or using another host's secret. | Satisfied for dataset and arrival boundary; validation later |
| SYNC-01: account/offline/conflict/deletion behaviour | Apple documents eventual/system-dependent syncing and separate app error responsibilities. | An offline edit, deletion on another device, sign-out or disabled Keychain can prevent convergence despite prior success. Data isolation is required, but local-use/account/recovery presentation and retention are incomplete. | Open — sync failure and data lifecycle |
| SYNC-01 / SESSION-02 / AGENT-03: two-device execution ownership | Synced history must not execute actions; host-side ownership is only a proposed design. | An iPad can receive an active task while its iPhone coordinator is still running. Replication alone neither grants takeover nor proves the old owner stopped. Explicit handoff/read-only/concurrent-control behaviour is unagreed. | Open — cross-device behaviour |
| PERF-01: responsive terminal and agent experience | Explicit central problem; no measured speedup or user-selected numeric budget exists. | Fast rendering can coexist with slow network echo, host work or model response. Representative workloads/conditions and acceptable observable response still need definition; no universal native/remote speed claim is supported. | Open — measurable acceptance |
| SETUP-02 / MODEL-01 / AGENT-CLOUD-01: later automation/routing/cloud management | User placed these outside MVP or in later research. | Their design uncertainty must not silently add a remote agent, automatic host changes or routing policy to MVP. Current roadmap retains them separately. | Satisfied for MVP deferral; later scope unresolved |
| CLOUD-01: cloud provisioning in version 1.1 or 1.2 | Explicit release-range direction. | Dropping provisioning entirely or making it an MVP onboarding prerequisite would contradict the choice. Provider/account/billing details remain future planning and do not prevent defining MVP. | Satisfied for placement; later planning incomplete |
| INTEGRATION-01: Warp-account feasibility investigation | Initial disposition found documented external cloud-run APIs; phone-account inference/mobile login remains unresolved. | Cloud-run control is not proof of an account-backed model endpoint for the phone agent. The research records that difference and keeps BYOK independent. | Satisfied for scoped research disposition; no working integration promised |
| Proposed quantitative guarantees and implementation claims | No app implementation, latency budget, speedup ratio or universal capacity is evidenced. | Passing document checks or saving a task cannot establish runtime behaviour. Remove implied passes and derive later budgets with declared units/workloads/evidence rather than invented numbers. | Satisfied for current evidence labelling |

**Coverage:** All 23 named requirements, their existing acceptance examples, the problem/placement summaries, glossary and material runtime/sync deferrals were examined. The Open entries name exact acceptance or factual contract gaps; the matrix does not treat an accepted direction as a completed detailed promise. Future-only research/placement is reviewed separately and does not silently expand MVP.

**Readiness result:** Clarification ongoing. Main scope is stable, but complete terminal/baseline and responsiveness acceptance, prepared-host boundaries, recovery/history, agent lifecycle and cross-device/account outcomes remain open. Compiler/SSH/store-library selection and future implementation testing are not themselves unanswered product questions.

## Understand handoff

Clarification ongoing. We comprehensively know the product direction and principal MVP inclusions/exclusions, but cannot yet mark the whole MVP Ready for Design under the Understand skill. Close the Open claim-level acceptance gaps, reconcile all affected records, and present the bounded requirement recap for product confirmation. Technical research and Design-owned choices proceed independently where they do not assume unanswered product behaviour.
