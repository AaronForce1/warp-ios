---
name: plan-delivery
description: Turn agreed software requirements and solution design into a repository roadmap and manageable implementation phases, with dependencies and completion evidence. Use for the Plan stage, planning the next phase, or replanning affected work after a change.
---

# Plan Delivery

Make the requested bounded change understandable and executable by a human or agent in a later session. Produce one current roadmap and task breakdowns for every phase within the requested planning scope, using linked phase documents only where useful. Preserve the agreed requirements and design while deciding the order and size of the work. Planning records describe intended work; they do not establish implementation or verification.

Read the relevant stage of the [bundled workflow](../_shared/development-workflow.md), alongside applicable project instructions. Project records use the project’s declared locations; bundled references resolve relative to this skill, not to the project’s docs folder.
Read the [bundled delivery contract](../_shared/delivery-contract.md) for delivery handoffs, authority and checkpoint/resume rules. Apply project-specific constraints and actual user delegation.

## Start from the current agreement

Read applicable project instructions, the requested scope, the feature map and affected specifications when present, current requirements, design and its handoff, relevant vocabulary, and the existing roadmap. For an existing codebase, inspect the affected implementation and tests to establish what remains. Reuse supported completion evidence; neither a checked box nor the existence of code proves completion.

Identify the authoritative records and the version or working-tree state used for planning. Link existing requirement IDs, design elements and boundary rules; use section links when IDs are absent. Keep substantive requirements and architectural decisions in their owning documents rather than duplicating them in task prose.

Respect prior agreement and delegation. Clarify only uncertainties that change the scope, sequencing or ability to start the next work. A material requirement or architecture change returns that point to Understand or Design, while independent planning continues. A later decision may remain open with its affected work, decision point and dependency made explicit. Do not reopen the entire interview or require future phases to be exhaustively designed.

Use the project's record locations. Defaults are `docs/ROADMAP.md` and, when needed, `docs/phases/<stable-id>-<name>.md`. This skill supplies [a roadmap template](assets/roadmap.md) and [a phase template](assets/phase.md). Adapt existing records before introducing new files. A small change can keep its tasks and handoff in the roadmap.

## Shape useful phases

Propose phases around observable outcomes that can be demonstrated or checked. Prefer an early, narrow path through the relevant components, then expand it. Genuine setup, research and migration prerequisites may be separate tasks; explain what they enable. Avoid a long sequence of disconnected layers that postpones integration and feedback until the end.

For a request to plan an agreed feature or change, give every phase an outcome, scope, task breakdown, dependencies and completion evidence before handing over the plan. The next phase may have finer detail, but later phases still need reviewable tasks. A predecessor that has not been implemented blocks execution, not planning its dependants. Small phase plans may stay in the roadmap; a separate file per phase is optional. Do not prescribe every future file or function merely to add detail.

Leave work as an outline only when the user requests that depth or a specific unresolved decision prevents a useful task breakdown. Record the affected scope, why its detail is deferred, and the decision or evidence that will unlock it. Being later in the sequence is not itself a reason to defer planning. Identify unfinished planning explicitly, while continuing to plan independent work. If the user requests only one phase, keep to that scope. Future product ideas outside the agreed change remain roadmap items rather than expanding this planning request.

Size tasks so their result can be explained, reviewed and verified without depending on the original conversation. Split work where responsibility, uncertainty or review size justifies it. Do not invent a fixed task count, time estimate or universal context-window limit. Discuss consequential priority or scope tradeoffs with the user; routine decomposition can use the agent's judgment.

Declare actual prerequisites by stable phase/task reference, not just list order. Mark work as suitable for parallel execution only when dependencies are satisfied and shared interfaces, state and editing areas permit it; separate files alone do not prove independence. A plan can describe parallel opportunities without authorising delegation or starting workers.

## Keep progress legible and coordinate parallel work

Keep one concise roadmap across the build, preserving unrelated features and supported completion history when planning a new change. Link capability specifications and detailed phases instead of copying their requirements. Show each active feature or phase's outcome, current delivery state, owner or unassigned status, dependencies/blocker, and a link to task detail and evidence. Keep lifecycle readiness separate from delivery progress.

Use icons with text: **⬜ Planned**, **🟡 In progress**, **🚧 Blocked**, **🔎 Verifying/reviewing**, **✅ Complete**. Label Deferred and Cancelled separately; neither is Complete. A green tick requires the scoped acceptance, configured checks, applicable review and integration evidence. A worker's completion message alone is insufficient. Do not present task-count percentages as measured product completion. Keep updates focused on meaningful state changes.

When parallel execution is requested or being planned, identify a coordinator and bounded work assignments. Each assignment names its task IDs, owning agent/role (or unassigned), scope and edit areas, shared interface agreements, prerequisites, expected evidence and return artifact/report. Plan separate writable areas or isolated worktrees where appropriate; shared contracts and files need a named writer or an explicit edit/integration sequence. Feature separation alone does not establish safe parallelism.

The coordinator maintains the shared roadmap and reconciles worker reports; workers update their assigned records or return results to the coordinator instead of concurrently rewriting the overview. Give integration and combined verification an explicit owner and closing task. Record blockers and missing evidence rather than counting an absent or failed worker as success. On resumption or reassignment, reconcile actual work and evidence before changing ownership or status. A plan defines these responsibilities; it does not launch agents or grant execution authority.

For a single-agent change, that agent can own the same responsibilities without a separate orchestration layer. Keep assignments inside existing task/phase records; no additional tracker or runtime is required.

When execution skills are available, make the plan usable by Implement, Review Change and Orchestrate Delivery through the bundled delivery contract and applicable project conventions. A worker assignment should be derivable from its task without replaying the planning conversation. Keep integration ownership and merge/release authority distinct from task ownership; workers do not receive those privileges. Planned parallelism does not start agents.

## Make tasks actionable

Carry forward [project preferences](../_shared/project-preferences.md) and apply the [verification policy](../_shared/verification-policy.md). Plan setup for selected missing skills/tools within the agreed scope, using the chosen package manager. Include a narrow running user journey early for web applications, then extend meaningful acceptance coverage. Assign browser/visual review and any live-service checks with their actual access dependencies. Use focused lower-level tests for risks they expose efficiently; avoid test-count targets, redundant matrices and duplicating every assertion across layers. Keep the check contract in one linked conventions record.

For each task, record, compactly:

- A stable ID, the intended change and its scope, including affected design elements or source areas where known.
- Links to the requirements, design rules or necessary enabling work it supports.
- Prerequisites and unresolved decisions that actually block it.
- Owner or unassigned status; for parallel work, edit scope, shared-contract dependencies and integration responsibility.
- Observable acceptance conditions and the tests, checks, inspection or delivered artifact that will demonstrate them.
- Current delivery status and, only when obtained, evidence of completion.

Use existing source mappings for orientation and label proposed locations. Specify contracts and constraints the implementer must preserve; leave routine implementation choices open. Do not generate application code, speculative class hierarchies or a second detailed design to fill out task descriptions.

Keep required behaviour tests and applicable quality/security checks with the work that needs them. Include integration and failure scenarios relevant to the selected scope. Cross-cutting checks may be shared if tasks link to them and the sequence makes clear when their evidence is required. Do not postpone all verification to a final cleanup phase.

Carry the design's verification approach into concrete work: configure missing agreed checks, run available checks, derive observed code-structure views, and compare them with the intended design. Name where the observed view and comparison will be recorded, with source links, extraction/inspection method, coverage limits and the actual source snapshot, including uncommitted work when applicable. Compare the affected elements and relationships with the intended model and record missing, extra or changed structure. A small source-linked table can be sufficient; directory names or a passing boundary check alone do not establish design conformance. Preserve human navigation from requirement to design to task to evidence. Distinguish automated results, AI assessment, human review and unresolved claims.

Reference real configured commands where available. If a capability is only proposed, record the setup work, its availability and what remains unverified; do not invent a working command, passing score or substitute for a required check. TypeScript and Rust may need different tools and evidence. Metrics retain the scope and limitations recorded in the design and project rules.

## Existing systems and phased refactoring

When applicable, preserve agreed behaviour with appropriate regression evidence. Describe the current and target structure, how they coexist during migration, and the tasks that move consumers and retire the old form. Link the design rather than designing a replacement here.

For each temporary exception, state its scope, reason, authority, verification impact and removal condition/task. Sequence the change so each claimed deliverable has meaningful checks. If intermediate work cannot be independently verified, identify the integration dependency and keep that work visibly incomplete until its combined evidence exists. Planning an exception does not approve it or relax an existing gate.

## Review the plan and hand it over

After drafting, perform a distinct review of the saved plan before handoff. Start from the original scope, requirements, design, project instructions and workflow. Derive the material obligations from those inputs before reading the plan's coverage claims; do not limit the review to obligations the drafter chose to mention. Include applicable verification, architecture comparison, documentation and completion work as well as product behaviour. Map each obligation to closing tasks and planned evidence, or record it as partial, missing or explicitly deferred with a reason and resolution point. Reuse phase exit sections and the roadmap rather than creating a parallel specification or mandatory review document.

Prefer a fresh reviewer agent when available and permitted by the environment and project instructions. Supply the requested scope, original inputs, saved plan and this skill's review criteria; let it assess them without the drafter's conclusions or suggested findings as an answer key. Otherwise perform a separate self-review pass by rereading the original inputs. Record which method was used; self-review is not independent review, and either method can miss defects. The reviewer identifies findings; the planner applies corrections. This review remains part of Plan and adds no human approval checkpoint.

Across every phase in scope, confirm there is a task breakdown or an explicit, justified deferral. For each material obligation derived from the inputs, record a compact closure review in the phase exit section or roadmap. Missing tasks stay visible in that mapping. Link existing tasks and shared checks rather than duplicating detail. A category-wide statement that completion or evidence was reviewed is insufficient. Record:

- **Outcome and closing work:** the observable promise, closing task or tasks, and a concrete planned acceptance scenario (setup/action/expected result, or equivalent inspection evidence). If behaviour spans tasks or phases, identify where the combined result is checked. Prerequisite work alone cannot close the requirement.
- **Evidence boundary and limits:** where the proposed check observes the result, and which relevant behaviour it bypasses through mocks, fixtures or separate checks. Testing an internal calculation or a caller with its transport mocked does not establish the separately mapped or displayed result. Distinguish controlled scenarios from live connectivity checks; retain the intended architecture comparison's method and limits.
- **Counterexample and resolution:** ask whether the proposed checks could all pass while the promised outcome is wrong. Challenge them with a concrete, relevant boundary or failure case. Record the gap found and the task/check changed to catch it, or explain how the proposed evidence would detect that case. A claim that no gaps were found, without that reasoning, is not a completed review. This assesses planned evidence; it does not report a test as run.

When a counterexample exposes missing evidence, update the task and acceptance check at the responsible boundary, or label the contribution partial and name the remaining outcome and closing work. Keep unresolved evidence gaps explicit; do not rewrite the requirement to fit the proposed tests. Use proportionate checks, reusing scenarios across obligations where each outcome is traceable, without enumerating every hypothetical failure or mandating a new test framework.

Reconcile full/partial claims and closing references across tasks, phase exits and the roadmap. Carry earlier guarantees forward for rechecking when later integration can invalidate them. Assign relevant documentation and delivery-status updates to the work that changes them. Reconcile task prerequisites with narrative sequence and verification setup; distinguish what is needed to start from what is needed to finish. Check dependency cycles, shared configuration edits in proposed parallel work, and decisions blocking the next scope. Confirm assignments have compatible edit ownership, that someone owns integration and combined verification, and that roadmap status agrees with the linked evidence. Missing integration cannot be hidden by completed worker tasks.

Apply the review findings to the tasks and checks, then recheck the affected obligations, dependencies and coverage claims against the saved corrections. Acknowledging a finding or adding a reassuring summary does not resolve it. Record the correction and its location, or the remaining gap and affected scope; do not claim full planning coverage while required work or its planned evidence is missing. A later gap may remain with its owner and dependent task identified while independent work proceeds. If an uncertainty cannot be resolved within the authorised scope, leave that part incomplete and identify the decision needed instead of repeating review indefinitely. Summarise the review method, actual corrections and remaining limits in the handoff, linking the closure reviews.

Present the sequence, first executable task, consequential tradeoffs and remaining decisions. Follow existing project instructions and user authority for agreement; this skill adds no mandatory approval system. Reconcile changes in the affected roadmap and phase records. State whether the whole requested planning scope is covered separately from which phase can execute next. Readiness to start the first phase does not establish that the full planning request is complete. Keep one planning status for each scope being reported:

- **Planning in progress:** breakdown or a material dependency still needs resolution.
- **Awaiting agreement:** only an applicable human planning decision remains.
- **Ready for implementation:** the named execution scope has actionable tasks, defined evidence and satisfied decision/approval prerequisites. Later phases may have complete plans while awaiting predecessor work. Justified outline-only work remains explicitly incomplete in the planning coverage statement.

Readiness does not mean tasks are delivered or checks have passed. Keep new task checkboxes open; mark complete only after acceptance, required verification and applicable review are evidenced. Cancellation and deferral are different from completion. A task finished to a limited scope does not make a larger phase complete while its integration or required review remains outstanding.

End with links to the current records, the next task and its prerequisites, the planned verification, unresolved dependencies, and the boundary of authorised continuation. A request to plan stops at this handoff. Continue to implementation only when it is already requested; invoking the skill does not authorise commits, publishing issues, live integrations or further implementation by itself.

For the next feature, fix or refactor, update the existing roadmap and affected open plans. Preserve unrelated work and supported completion history. Reassess affected tasks and evidence when requirements or design change. Summarise completed phases in the roadmap and keep details only while useful; Git preserves earlier versions. Tracker issues are optional links to these repository records and require explicit publication authority.
