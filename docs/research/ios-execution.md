# iOS terminal execution: initial feasibility evidence

This is source-based research for requirements discovery, not an approved architecture or a device test. It addresses the user's requested native interactive terminal and the premise that ARM-native user-space execution alone would yield desktop-terminal parity.

## Distinctions

1. **Terminal interaction and rendering:** Input, terminal control sequences, scrollback, and session UI are separate from where commands execute. A native terminal can connect to a remote shell without running that shell locally.
2. **Native local command implementation:** Programs adapted and packaged as signed app code can execute locally without x86 emulation. Existing maintained projects demonstrate this approach for particular commands; they do not establish compatibility for every desktop tool.
3. **General desktop process environment:** Arbitrary executable loading, ordinary shell process creation, job control, package installation, and indefinite background execution are separate obligations. ARM instruction compatibility does not grant these operating-system capabilities.

## Sources and scoped findings

- [Apple Platform Security: App code signing process](https://support.apple.com/guide/security/app-code-signing-process-sec7c917bf14/web). Apple documents mandatory signing of executable code and prevention of unsigned-code loading. This is an operating-system constraint distinct from app review; it does not prohibit every interpreted program or establish the capabilities of a specific interpreter.
- [Apple App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/), particularly 2.5.2 and 2.5.4. These describe restrictions on downloaded functionality and background services, with stated exceptions. Read current rules against the actual product and distribution model; no App Store approval or rejection has been established for this application.
- [ios_system maintained implementation and porting guidance](https://github.com/holzschu/ios_system). It implements commands through embedded frameworks and replacements for command execution APIs. Its guidance identifies incompatibility with ordinary fork/exec-style execution and required command adaptations. This supports native command execution as a candidate and argues against assuming unmodified desktop process behaviour. Its individual historical command limitations are not universal platform conclusions.
- [a-Shell maintained implementation](https://github.com/holzschu/a-shell). It provides a concrete iOS terminal using ios_system and bundled languages, with separate WebAssembly execution for additional compiled programs. Its documentation reports App Store availability. This is contrary evidence to a blanket claim that iOS terminals require x86 emulation or cannot run local commands. Availability does not prove all desktop capabilities or guarantee approval for our app.

## Consequences for discovery

Do not reduce the user's request to a remote dashboard. Retain direct interaction, native local execution, SSH, infrastructure workflows, and the agentic overlay as requirements to refine.

Evaluate each required command and behaviour individually. kubectl needs investigation of the iOS embedding/build approach, networking, credential formats, and external authentication helpers; no native kubectl result has been demonstrated. A remote shell is an alternative for unsupported local operations, not an already-approved substitution.

The next architecture should compare a native command catalogue and remote execution adapters against the exact agreed command and interaction contract. A shell-like runtime may implement selected semantics in-process, but must not claim ordinary OS process isolation, unrestricted packages, or full desktop compatibility without evidence.

## Evidence limits

No iOS build, simulator, physical-device command execution, interactive terminal compatibility suite, or App Store review was performed. The cloud machine is Linux without Xcode. Public documentation and maintained implementation guidance establish scoped options and constraints, not a finished design or a universal impossibility proof.

## Linux distribution images and the iSH comparison

- [iSH's maintained description](https://github.com/ish-app/ish) explicitly identifies user-mode x86 emulation **and syscall translation**. This confirms that it addresses both instruction execution and the Linux operating-system interface. The user's performance report has not been independently benchmarked.
- [Docker's container explanation](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/) states that containers share their host kernel. Pulling a Debian/Ubuntu ARM image supplies a userspace filesystem; it does not supply a running Linux kernel or make Linux system calls available inside a normal iOS app. A concrete local design needs an independently validated compatibility/interpreter/virtualization mechanism, rather than treating image extraction as execution readiness.
- A terminal connected to a personal-computer/cloud Linux environment is a supported candidate consistent with the user's latest permission. Selecting a host whose architecture matches its images avoids instruction-set emulation on that host. End-to-end responsiveness still depends on host resources, transport, mobile rendering, and workload; no performance pass has been demonstrated.

**Agent recommendation, not an agreed release requirement:** evaluate a native iOS interactive client with a real Linux execution backend for the first end-to-end milestone, while assessing local native commands as a separately scoped capability. Do not substitute this for offline local Linux parity unless the human agrees to the first-release connectivity contract.

**Product decision now confirmed:** requiring a connection is acceptable for the first release. The remote execution candidate is within the accepted release boundary; exact host provisioning, ownership, session continuity, and performance acceptance remain unresolved. Next clarify the first user onboarding journey.

## Session persistence and mobile recovery

[tmux's maintained documentation](https://github.com/tmux/tmux) describes detached terminals that continue running and can later be reattached; its documented platforms include Linux and macOS. This supports tmux as a candidate for the scaffolded baseline. GNU Screen is the user's suggested alternative; its official manual request failed during this research, so no current manual-based claim is made here.

Disconnect/reconnect support in the desktop Warp repository was located in `crates/remote_server`, but source discovery is not proof of terminal survival after iOS process termination or permission to execute the same subprocess-based SSH client on iOS. Portability, protocol reuse, and licensing require separate assessment before adoption.

A persistent remote session needs remote capability and an app-restorable session identity. A reconnect must not replay side-effecting commands with unknown outcomes. Detached terminal support does not by itself establish transcript retention, agent conversation-state persistence, host-reboot recovery, or compatibility with every SSH server.

No live multiplexer, SSH interruption, or iOS relaunch test has been executed. These are planned outcome-level validation obligations. The user has confirmed that existing hosts are prepared by a repository script, with MVP instructions in the app. Automatic setup over SSH is a desired later convenience. Verification of persistence capabilities and compatibility remains outstanding.

## Server provisioning standard

[Official cloud-init documentation](https://cloudinit.readthedocs.io/en/latest/) describes first-boot initialization, including SSH keys, packages, networking and storage, across multiple providers and distributions. This supports cloud-init as the user-requested provisioning format; it does not prove our future template works on every provider or existing computer. A repository bootstrap for existing hosts and cloud-init for fresh supported servers should share an agreed readiness contract. Validation requires an actual prepared host and application connection, not only template syntax.

## Initial AI integration evidence

The desktop checkout contains provider-credential/custom-model configuration in `crates/ai/src/api_keys.rs` and authenticated public-service request helpers in `crates/warp_server_client/src/public_api.rs`. These are concrete research leads, not a supported iOS integration contract. Its remote transport also uses spawned SSH processes in platform-specific paths, so direct mobile reuse requires investigation rather than assuming native iOS can execute the same client.

[OpenRouter's official quickstart](https://openrouter.ai/docs/quickstart) describes a unified model API and links routing/provider-selection capabilities. This is a reference for the user's later model-routing direction, not a decision to make OpenRouter a dependency or proof that switching providers preserves agent state/tool behaviour.

Required Warp feasibility work: identify official supported developer access and account flows, assess mobile authentication/API compatibility and model/agent access, review source-reuse licensing, and isolate any external prerequisite. Mark live access unverified unless exercised with authorized credentials. BYOK remains the independent MVP path. No provider keys or account secrets were requested or used in this research.

## Phone agent coordination versus remote execution

[Apple: Extending background execution](https://developer.apple.com/documentation/uikit/extending-your-app-s-background-execution-time) describes suspension and limited extensions; it does not promise arbitrary uninterrupted execution. Contrary evidence to an overly broad “iOS cannot run background work” claim was sought: [Apple's continued-processing task request](https://developer.apple.com/documentation/backgroundtasks/bgcontinuedprocessingtaskrequest) explicitly supports user-initiated work continuing after the app backgrounds. Applicability, supported OS versions, task limits/expiration, and real-device behaviour need assessment. No background-execution experiment has been performed.

The relevant states are foreground, permitted background execution, suspension, and termination; these must not be collapsed into one “closed app” case. A terminated coordinator process is not running. Persisted state may support resuming later, while commands in a separately persistent remote session continue. This is distinct from requiring a remotely hosted agent. The user's default-continue preference and phone-owned runtime must be reconciled through an explicit product pause/resume contract; do not claim universal background continuation or rule out supported APIs without investigating them.
