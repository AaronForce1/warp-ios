# Proposed MVP acceptance requirements

**Understand status:** Clarification ongoing.
**Agreement:** Proposed additions to the established MVP; awaiting the user's confirmation by numbered group or individual clause.
**Delivery:** Requirements only. Targets below are proposed acceptance gates, not measured results or assertions that the current candidates meet them.
**Authority:** The user requested initial requirements for the five readiness gaps. Existing confirmed scope remains in the [product foundation](product-foundation.md).
**Related records:** [Glossary](../GLOSSARY.md), [readiness review](product-foundation.md#readiness-review), [architecture](../design.md), [phase plan](../phases/mvp.md).

Approve a complete group, or refer to a clause such as **3.3** when requesting a change. Engineering selection, protocol design and instrumentation remain the agent's responsibility.

## 1. Terminal capabilities and host baseline

**Proposal:** deliver the common interactive terminal capabilities needed for development and operations through a prepared remote host.
**Parent requirements:** TERM-01, TERM-03, TERM-04, SSH-01/02, SETUP-01, EXEC-02.

**1.1 Interactive terminal.** Support UTF-8 text including CJK and emoji, ANSI/VT100/xterm-style cursor and screen control, 256 colours and true colour, alternate-screen applications, window resizing, shell pipelines/redirection and normal shell job control. Preserve the selected remote shell's working directory, environment and foreground program. User-entered commands run directly; the agent approval setting governs agent actions.

**1.2 Mobile interaction.** Support selection/copy/paste, scrollback search, Tab, Escape, arrows, Ctrl combinations and hardware keyboard input on both iPhone and iPad. Fullscreen applications such as `vim` and `top` must remain usable through input, rotation/resize, session switching and reattachment. Paste must respect terminal/application modes rather than being interpreted as an unintended sequence of submissions.

**1.3 Reference Linux environment.** Validate repository provisioning against Ubuntu 24.04 LTS and Debian 13 on their native supported x86-64/ARM64 hosts. Include an interactive Bash environment, standard file/text/archive tools, Git, curl, Python 3, an editor/process viewer, kubectl, SSH access and the persistence capability. Package installation uses the host distribution's normal package manager and the user's host permissions. Cluster credentials/configuration belong to the user's host; installing kubectl alone is not Kubernetes access.

**1.4 Existing-host contract.** A host is ready only after direct password/key SSH, an interactive terminal and app-compatible persistence/identity/recovery capabilities pass readiness checks. The repository must provide existing-host preparation and fresh-server cloud-init. Preserve host-OS-independent connection scope, including relevant macOS/Windows SSH environments; their tools/shell remain host-specific. Preparation must identify incompatible/missing capabilities and give specific remediation rather than falsely claiming readiness or forcing every host to become Linux. Exact library/key-format/platform adapters are engineering work and still need feasibility evidence.

**1.5 Parity boundary.** MVP parity covers the interactive command-line behaviours above. Desktop GUI applications, iTerm-specific plugins, inline image/video protocols, local iPhone Linux execution and a Docker daemon on the phone are outside this proposed baseline. Remote tools installed on a capable host can still be invoked normally. Existing exclusions—bastions, SSH MFA and forwarding—remain unchanged.

**Acceptance examples**

- Open a prepared Linux host; change directory/export a variable, run a pipeline and edit a file in vim. After rotating and switching to another session, return with the same context and correctly rendered application.
- Query a controlled Kubernetes test context and handle a remote credential-helper prompt/failure as terminal interaction. Do not claim a working workflow from kubectl help or installation alone.
- Connect to a host where authentication works but persistence preparation fails. Show the missing prerequisite and instructions; do not present it as a durable-session success.
- A direct macOS/Windows host is evaluated against the prepared-host contract, not silently excluded because the baseline cloud-init template is Linux-specific.

## 2. Responsiveness and performance targets

**Proposal:** make local interaction fast and measure terminal/network/provider costs separately.
**Parent requirements:** PERF-01, TERM-01, PLATFORM-01, AGENT-03.

**2.1 Local responsiveness.** Local navigation, session selection and approval controls should provide visible feedback within **100 ms at the 95th percentile**. A received terminal/model update should become visibly rendered within **50 ms at the 95th percentile**. These targets measure application processing, not waiting for a host/model to respond.

**2.2 Typing and attachment.** On the reference network, typing-to-remote-echo should be **150 ms or less at the 95th percentile**. A cold launch should show locally saved sessions within **2 seconds**, and connecting/reattaching to a prepared saved host should reach an interactive state within **5 seconds**. The attachment gate assumes usable saved credentials and an already-trusted host; time the user spends entering credentials/trusting a host is separate.

**2.3 Output load.** While processing **10 MiB of text at 1 MiB/second**, the app should maintain the local interaction targets and correct current terminal state. This is a 10-second representative workload, not a universal throughput/capacity guarantee. Old scrollback may trim under 3.3; incoming control sequences/current-screen output must still be processed correctly rather than dropped to make the metric pass.

**2.4 Model/network visibility.** Show working/waiting/streaming status promptly; maintain usable manual-terminal and Stop controls while a provider is slow. Measure provider first-response time, remote command time, network RTT and app rendering separately. Do not promise an arbitrary provider reply or remote compute result within the local UI budget.

**Test conditions and rationale.** Use release builds on both form factors, including the slowest supported reference devices chosen during Design. For the typing/attachment gates use a healthy prepared host with round-trip latency of **50 ms or less** and no induced loss; report actual host load/device/OS/network. The 150-ms echo budget allows 50 ms of network time plus up to 100 ms of combined endpoint handling. Test poor connectivity separately for correct status/recovery; those conditions do not inherit the reference-network echo deadline. Report measured samples and percentiles rather than labelling a single fast interaction as a pass. These are product budget proposals; device/library feasibility remains unmeasured.

**Acceptance examples**

- A long-output command runs while the user changes tabs or approves an action. Controls meet the local feedback budget, and the current terminal screen stays accurate.
- Delay the model provider response. The app shows waiting state and can stop the agent without freezing the terminal; the report identifies provider latency rather than calling it terminal-rendering time.
- Introduce a high-latency/disconnected network. Show the actual connection state and recover under group 3 without promising the healthy-network echo target.

## 3. Recovery, history and deletion

**Proposal:** preserve live remote work across phone interruptions, with explicit limits for host failure and retained output.
**Parent requirements:** SESSION-01/02, SYNC-01, AGENT-03.

**3.1 Client interruption.** Locking the phone, switching apps, losing connectivity or terminating/relaunching the app must not end the remote shell/foreground job while the host persistence mechanism remains alive. Restore the actual named session, current directory/environment and running interactive application. Switching among saved sessions does not terminate other sessions.

**3.2 Ambiguous results and host failure.** After reconnect, reconcile what the host accepted/completed before starting new actions. Never automatically replay an uncertain command or uncertain terminal input. Distinguish unreachable/unknown host state from a confirmed lost session. If the host reboots or its persistence process is lost, report session loss and offer an explicit new session; do not claim process restoration or restart old jobs automatically. Keep saved app records/history even when the live process is lost.

**3.3 History default.** Keep agent conversations and their command/result history until the user deletes them; synchronize that history as agreed. Keep raw terminal scrollback **locally**, with a proposed default of **10,000 rows or 20 MiB of stored terminal content per session, whichever is reached first**. Expose the configured limit and history clearing. These are retention bounds, not a claim that total RAM is 20 MiB. Long-term full terminal recording/cross-device raw transcript archives are deferred. A second device receives the remote current screen/available host scrollback, not a guarantee of all past terminal output.

**3.4 Deletion semantics.** Deleting conversation/history/host/credential records propagates when synchronization is available; older offline edits must not silently resurrect deleted records. Removing saved app data detaches related local use as needed but does not kill remote jobs. Ending a remote session is a separate explicit operation. Removing a saved credential does not revoke the upstream provider key or change the host's password. Account quota/sync errors keep unsynced local records and show a recoverable state instead of silently discarding work.

**Acceptance examples**

- Force-terminate the app while vim has an unsaved buffer and a second session has a foreground job. Relaunch/reattach: the buffer/job remain on the live host and the correct sessions are shown.
- Drop the response after a command changes a test file. Reconnecting reports the recorded outcome or an unresolved state and does not apply the change a second time.
- Reboot the host. Show that the previous session is gone while preserving its saved identity/history; create a fresh shell only on the user's explicit action.
- Produce more scrollback than the retention default, and delete a synced conversation while another device is offline. Trim only old retained output; after reconnection the deleted conversation does not return from a stale update.

## 4. Agent authority and lifecycle

**Proposal:** keep the phone coordinator visible, interruptible and bound to the user's task/session.
**Parent requirements:** AGENT-01/02/03, AI-01, SESSION-01.

**4.1 Task and approval scope.** Define an agent task as one user objective bound to the named host/session. The agent may use terminal commands, inspect/edit files and run checks through that host account to achieve the objective. Changing the target host/session or expanding a diagnosis-only request into a repair requires an explicit scope change. An objective already requesting a repair permits the required changes under the selected approval mode.

**4.2 Approval mode.** Proposed default: **task-level approval**, with per-command approval available before a task starts and in settings. Task approval shows the objective/target; per-command approval shows the proposed command and target before dispatch. A refusal never sends the command. Synced preference changes apply to new tasks; changing an active task's mode is explicit and affects only undispatched work, invalidating stale pending approvals.

**4.3 Observable execution.** Show the active task's target, proposed/running commands, available output, result/exit state and completion/failure/unknown status. Execute in the selected session's working directory/environment rather than a separate default-directory shell. Distinguish incomplete/truncated output and interactive-input requests from completion. Do not claim a file change or successful action that has no supporting execution result.

**4.4 Stop and manual takeover.** Provide Stop and Take Control. Stop prevents further agent dispatch, invalidates pending approvals and cancels outstanding model work; request a normal interrupt of an identifiable agent-owned foreground command. Display interruption as requested/confirmed/unknown according to host evidence, rather than claiming every process obeys it. Take Control pauses new agent steps and gives the user terminal input without automatically killing the current remote program. Agent execution resumes only on an explicit user action after manual takeover. Allow one active agent task per session; different sessions may each have a task when runtime is available.

**4.5 Continuation and failure.** The existing continuation setting defaults **on**. Attempt eligible background work while iOS grants runtime; pause new steps when execution/connectivity is unavailable while already-running remote work continues. After return, default-on tasks may resume only after reconciling the same host/session, current ownership, approval mode and prior command outcome. Pending per-command approvals still wait. Uncertain outcomes, manual takeover or changed ownership require an explicit resume/decision. Missing/invalid keys, provider failures and rate limits preserve task progress and offer recoverable retry/configuration; never silently switch provider/model or replay terminal actions to recover. Provider errors do not break the manual terminal.

**4.6 AI context and disclosure.** Before first agent use, explain that the selected external model provider receives the user's instructions and task-relevant terminal/file content. Scope automatic context collection to the approved task and selected session; do not attach unrelated sessions/conversations or the credential store. SSH passwords/private keys and provider API keys must not be included as model context or application diagnostics. Send the selected provider's API key only through its required authentication mechanism. Terminal/file content can itself contain sensitive data: filter recognized secrets and disclose that arbitrary secrets cannot be perfectly detected. Manual terminal use does not by itself send its output to a model. These are proposed product data boundaries, not a claim that a filter or provider privacy policy has been validated.

**4.7 Elevated and destructive actions.** Proposed default: task approval permits ordinary actions within the approved objective, but agent-requested privilege escalation, disk formatting and deletion of an entire project/environment require separate explicit confirmation showing the target and action. This is a proposed exception to task-level approval, not an already agreed restriction. Route host password/credential prompts through direct user input, never through model context or a saved-password tool argument. Refusal pauses that step without dispatch. Existing host privileges still determine what can run; the app cannot infer authority from terminal output or guarantee detection of every destructive shell expression. Design must define the supported operation boundary and validate enforcement rather than promise a universal shell-command classifier.

**Acceptance examples**

- Approve a multi-step repair in task mode: commands within the approved scope execute without routine per-command prompts, subject to the proposed exceptions in 4.7. In command mode decline a proposed change: no dispatch occurs.
- Enter a fullscreen program or take manual control during an agent task. The agent does not send its next command into that program as if a shell prompt were ready.
- Stop a task while its provider/remote action is pending. No later model response starts another command; the UI accurately distinguishes an interrupted process from a process still running.
- Terminate/relaunch with a pending approval or lost result. Restore the task, reconcile the host, and keep uncertain work/pending approval from being automatically re-executed.
- Run a manual terminal command containing a test secret: manual use makes no model request. Start an agent task and inspect a controlled provider request: it excludes the credential store, unrelated session content and recognized test secrets; provider authentication remains separate from prompt content.
- In task mode propose sudo or deletion of a whole test project. Show separate confirmation; declining sends no action. If a host password prompt is needed, direct input reaches the host without becoming model context.

## 5. Cross-device control and iCloud availability

**Proposal:** sync data and credentials while keeping active execution ownership explicit.
**Parent requirements:** SYNC-01, SESSION-02, AGENT-03, PLATFORM-01.

**5.1 Data and credentials.** Sync saved hosts, settings, session identities and agent conversations through the user's private iCloud app data; sync SSH credentials and model keys through iCloud Keychain. Limit this sharing to devices on the same account. App records carry stable credential identifiers, not secret values. Receiving records/credentials does not itself create a terminal connection or start an agent.

**5.2 One controller per session.** Within the app-managed session protocol, one device owns terminal/agent input at a time; other attached devices may view. Switching control requires an explicit Take Control action, with the previous owner's authority to dispatch revoked at the host boundary before the new owner can dispatch. If transfer cannot be established, remain view-only/blocked for input and show why. Controller changes may resize the terminal; viewers do not change its remote dimensions. Different sessions can have different controllers.

**5.3 Agent handoff.** Transferring terminal control does not silently start a second agent. The new device may explicitly resume a task only when it has the required checkpoint and can reconcile remote command state/ownership. Otherwise show available history and unresolved state; do not fabricate missing task progress or replay old tool calls. Old-owner commands already accepted by the host may finish, but no newly dispatched old-owner action is accepted after transfer.

**5.4 Unavailable sync and accounts.** Allow local manual terminal/agent use with usable local credentials when iCloud/Keychain is unavailable or the user is not signed in. Show actual app-data sync state and credential availability; do not promise a Keychain delivery acknowledgement the platform does not expose. Queue eligible app-data changes for later sync. Missing credentials on a second device produce Credentials needed/waiting, with retry/manual configuration available. On sign-out/account change pause affected agent tasks and detach account-bound connections, preserving remote work. Hide the prior account's data/credentials and isolate its pending changes; retain protected prior-account local state for that user's return or explicit deletion rather than sending it to the new account.

**5.5 Conflicts.** Merge new sessions/conversation entries by stable identity. Surface concurrent connection/credential-reference changes when they cannot be reconciled safely. Do not silently retarget an active session when a host profile changes. Deletions defeat older stale updates unless the user explicitly restores/recreates the item. Scope active-task approval/control to its established state, not a stale synced preference or timestamp.

**Acceptance examples**

- An iPad discovers the iPhone's host/session/history and resolves synchronized credentials, then attaches to the actual remote session. If metadata arrives first, show the missing credential state rather than falsely reporting readiness.
- The iPhone is controlling an agent task; the iPad attaches as a viewer. After explicit confirmed transfer, only the iPad can dispatch new actions; restoring old phone data does not restart its agent.
- Use the app with unavailable iCloud, then restore it. Local work remains available and eligible changes reconcile without duplicated records or actions.
- Sign into a different account or deliver an offline conflicting edit. The prior user's data is not displayed under the new account, and the existing live connection is not silently redirected to an edited host.

## Proposal review and confirmation

**Review method:** distinct agent self-review of the saved clauses against the [existing claim-level matrix](product-foundation.md#readiness-review), agreed scope and linked research. This is not independent review or implementation validation. Each row names the draft claim, its basis/limit and a concrete challenge. All remain **Open** for the proposed additions; existing parent agreements are preserved. Numerical budgets are desired gates awaiting confirmation, not feasibility measurements.

| Clauses / material claim | Basis and evidence limit | Concrete challenge / draft result | Status |
|---|---|---|---|
| 1.1–1.2 Interactive terminal and mobile input | Desktop-like goal is agreed; compatibility cases are proposed. SwiftTerm is a documented candidate, not a pass. | A shell prompt can work while CJK, control keys, paste or vim after resize fails. The draft requires those cases, not prompt-only acceptance. | Open |
| 1.3 Distribution/tool baseline | Linux baseline is agreed; versions/tool list are an engineering proposal. | kubectl installation does not grant cluster access. The draft requires a real controlled workflow; architecture/package support still needs evidence. | Open |
| 1.4 Prepared, OS-independent host | SSH and preparation scope are agreed; platform capability feasibility remains open. | An authenticated host may lack interactive persistence. Readiness must fail with remediation; non-Linux support is not inferred from Linux cloud-init. | Open |
| 1.5 Parity exclusions | Existing advanced SSH exclusions are agreed; graphics/plugin limits are new proposals. | A user may interpret desktop parity as inline graphics or plugins. The draft explicitly asks to exclude these from MVP. | Open |
| 2.1 Local/render latency | New desired numerical budgets; no measurements exist. | External waiting can contaminate the timing. The draft measures local feedback and receipt-to-render separately. | Open |
| 2.2 Echo latency | New 150-ms p95 target under RTT ≤50 ms; feasibility unmeasured. | High RTT invalidates a universal echo guarantee. The gate is restricted to stated conditions and both endpoints must be measured. | Open |
| 2.2 Cold launch / attach | New 2-/5-second budgets; feasibility unmeasured. | Password entry or first-use host trust can dominate time. The draft separates human interaction from prepared attachment. | Open |
| 2.3 Sustained output | New representative workload; no capacity pass. | Dropping terminal control bytes can fake fast rendering. The draft requires correct state while processing 10 MiB over 10 seconds. | Open |
| 2.4 Waiting visibility / controls | Slow-model pain point; exact acceptance is proposed. | A responsive spinner can coexist with a blocked Stop control. Both Stop and the manual terminal must remain usable. | Open |
| 3.1 Live-host recovery | Client-interruption persistence is agreed; tmux evidence is scoped to a live host. | App termination with an unsaved editor must reattach to the actual process; opening a replacement shell is insufficient. | Open |
| 3.2 Unknown outcome / host loss | No replay is already agreed; reboot outcome is newly proposed. | A lost acknowledgement may follow a completed mutation; a reboot can destroy it. Reconcile the former, report loss for the latter, never silently rerun. | Open |
| 3.3 Conversation / raw-output retention | Conversation sync is agreed; indefinite-until-delete history and bounded local raw output are new proposals. | Bounded scrollback is not a complete archive. The draft names 10,000-row/20-MiB limits and excludes full cross-device raw recording. | Open |
| 3.4 Deletion / quota | Eventual sync is documented; desired deletion semantics are proposed. | An offline edit can resurrect data or a host deletion could kill work. The draft separates record deletion, upstream revocation and process termination; quota failures preserve local state. | Open |
| 4.1 Task authority | Agent execution is agreed; objective boundaries are proposed. | Diagnosis approval does not imply repair on another host. Scope change is explicit. | Open |
| 4.2 Approval default / mode change | Two choices are agreed; task-mode default and change semantics are proposed. | A stale synced toggle could change an active approval. Only explicit task-mode changes affect undispatched work. | Open |
| 4.3 Session context / results | Phone coordinator is agreed; detailed execution visibility is proposed. | A separate fresh shell can run in the wrong directory; partial output can hide an interactive prompt. Selected context and accurate result/input state are required. | Open |
| 4.4 Stop / takeover / concurrency | These observable lifecycle rules are proposed. | A late provider response or queued step can execute after Stop or enter a manual editor. The draft halts new dispatch and requires explicit resume after takeover. | Open |
| 4.5 Continuation / errors | Default-on where runtime permits is agreed; [iOS runtime evidence](../research/ios-execution.md) excludes coordination by a terminated process. Resume/error rules are proposed. | A pending approval or unknown command must not become an automatic retry. Reconciliation precedes continuation; provider failure preserves state without switching providers. | Open |
| 4.6 AI context / disclosure | The architecture already leaves disclosure/redaction undefined; BYOK is agreed, but these boundaries are proposed. No filter/provider privacy behaviour has been validated. | A manual terminal or unrelated session could be uploaded as context, and file output may contain unknown secrets. The draft limits automatic context and credential handling without promising perfect redaction. | Open |
| 4.7 Exceptional approval / credentials | The foundation explicitly leaves exceptional operations unresolved; additional confirmation is a product proposal. Enforcement feasibility is not established. | Task approval could silently permit sudo or whole-project deletion. The proposal requires a distinct decision and direct credential entry; it does not claim complete shell-effect detection. | Open |
| 5.1 Data / credential arrival | Datasets are agreed; [sync research](../research/native-stack-and-sync.md) documents distinct mechanisms/limits. | Metadata can arrive before a key. Stable references and actual credential availability are required; replication never starts work. | Open |
| 5.2 Host-bound ownership | Single-controller/viewer policy is proposed; enforcing host protocol is not implemented. | Two devices can both believe they own input. Transfer must revoke the old app controller before new dispatch; uncertainty blocks input. | Open |
| 5.3 Agent handoff | Explicit resume/checkpoint policy is proposed; transfer feasibility unverified. | A partial cloud checkpoint can omit accepted work. Incomplete state is shown, not reconstructed through replay; no automatic second agent. | Open |
| 5.4 Local use / key availability | Local-use policy is proposed; Apple does not expose a universal Keychain delivery receipt. | A missing secret must not be shown as synced/readied. Local usable keys permit work; unavailable credentials require configuration/retry. | Open |
| 5.4 Sign-out / account boundary | Account isolation is established direction; disconnect/retention behaviour is proposed. | Old pending changes can leak into a new account. Pause/detach, isolate protected prior-account records and preserve remote jobs. | Open |
| 5.5 Conflicts / identity | Proposed desired conflict rules; no merge implementation exists. | A stale host edit can redirect execution or restore a deletion. The draft keeps active targets stable and requires visible conflict/deletion handling. | Open |

**Coverage:** all numbered clauses in groups 1–5, including the added 4.6/4.7 data/authority boundaries, their acceptance examples, numerical conditions and material new exclusions were checked. This review maps new proposals to the parent matrix rather than replacing its Open findings with a category-level pass. Product confirmation settles desired behaviour; consequential factual premises remain separate, and implementation validation remains future work.

**Technical follow-through:** Design must select/pin the native/provider/host implementations, validate the named scope and proposed budgets, and define supported key/algorithm/model variants. Confirmation establishes desired product behaviour; it does not establish that a candidate has passed its tests. A confirmed requirement found infeasible must return for a scoped decision rather than silently being removed.

**Understand handoff:** Clarification ongoing. These proposals address the five gaps but are not agreed until the user confirms/changes them. Prepared-host/library/provider feasibility premises and the final scoped recap still need reconciliation under the existing workflow. No application code, external-host setup, signing or publication is included in this drafting task.
