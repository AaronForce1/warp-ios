---
name: review-change
description: Review an implemented change or pull request against agreed requirements, design and verification evidence. Use before integration or to recheck corrections; return a scoped acceptance decision and actionable findings without merging or changing the implementation.
---

# Review Change

Determine whether the identified implementation meets its agreed scope and required checks. Review the actual diff and relevant source, using original obligations to uncover work missing from the patch. Return evidence and actionable findings to the orchestrator or human. A review is bounded assurance, not a guarantee that no defects exist.

Read the relevant stage of the [bundled workflow](../_shared/development-workflow.md), alongside applicable project instructions. Project records use the project’s declared locations; bundled references resolve relative to this skill, not to the project’s docs folder.
Read the [bundled delivery contract](../_shared/delivery-contract.md) for delivery handoffs, authority and checkpoint/resume rules. Apply project-specific constraints and actual user delegation.

## Establish the review boundary

Read applicable project instructions, the bundled workflow and delivery contract. Locate the assignment, authoritative feature specifications, design, phase/tasks and configured checks. Use their declared locations and stable references. Preserve existing agreements; proposing a different design does not make an otherwise compliant patch defective.

Identify:

- Requested tasks and acceptance scope, exclusions and prerequisites.
- The exact base and head being compared, including relevant dependency branches. For uncommitted work, identify the base plus a reproducible snapshot of staged, unstaged and in-scope untracked content; a commit ID alone cannot identify dirty work.
- Edit ownership, shared interfaces and the integration boundary. A worker's bounded contribution can be reviewed separately, but cannot establish completion of the full feature.
- Available evidence, required checks and applicable human decisions. Ask only for missing input that materially prevents assessment, while reviewing independent areas.

Keep review read-only by default. Inspect files and evidence; run relevant safe checks within existing authority and isolation. Do not overwrite concurrent work or run commands that mutate a live service, publish results or expose credentials. If checks need unavailable access or an unsafe setup, identify that limit. Do not change code, specs, check settings or roadmap status as part of ordinary review. A requested review report may be written to the assigned output location; otherwise return it in the conversation.

## Derive obligations, then inspect the change

Use the agreed [project preferences](../_shared/project-preferences.md) and [verification policy](../_shared/verification-policy.md). Check applicable supporting-skill use and justified exceptions without turning personal style into a defect. For UI work, inspect the rendered result and key-journey evidence against the design; a DOM test or a startup screenshot is narrower than a running browser journey. Review changes to tests, rule configuration, exclusions and suppressions for lost obligations. High scores or test counts do not offset a missing outcome or a weakened gate.

First derive material obligations from the original scope, requirements, design and project rules. Then examine the patch and the worker's report. Do not let a task checklist or passing test summary define the entire review surface. Inspect surrounding callers, consumers, configuration and tests where they affect correctness; do not expand into an unrelated whole-repository audit.

Check the following where applicable:

- **Behaviour and omissions:** trace each material promise through its implementation and an observation that demonstrates the outcome. Include relevant failures, partial results and regression paths. Distinguish intentionally deferred scope from missing required work.
- **Architecture:** compare affected boundaries, dependencies and important code structure with the agreed design. Check source mappings and observed views against actual code; link source evidence for missing, extra or changed structure. Passing tests, directory layout or plausible diagrams alone do not establish conformance. A compact source-linked comparison is sufficient for a small change.
- **Clarity and testability:** assess responsibilities, interfaces and dependency handling against the project's standards. Patterns and SOLID guide judgment; do not demand additional layers or a named architecture without a concrete need or agreed requirement.
- **Verification credibility:** inspect what tests actually assert, which boundaries mocks bypass, and whether evidence applies to this snapshot. Challenge important claims with a concrete way the checks could pass while the outcome is wrong. Reuse relevant existing evidence and rerun checks to resolve material uncertainty; do not mandate exhaustive tests or arbitrary thresholds.
- **Configured quality and security:** inspect applicable rule results and relevant source, exceptions and regressions. AI judgment does not waive a failing required gate. Report future or unsupported analysis capabilities explicitly; do not invent commands, scores or universal new requirements.
- **Integration and records:** inspect shared-interface compatibility, dependency assumptions, documentation changes and delivery claims. An isolated worker result does not verify the combined branch. State what integration must still establish and which owner should close it.

Distinguish automated results, AI assessment, human review and unresolved claims. Evidence should identify its scope, method, result and snapshot; a link to a log without examining its applicability is insufficient. Do not repeat secrets or sensitive payloads in findings.

## Return a decision with useful findings

Use the project's report format or adapt [the review result template](assets/review-result.md). Keep the report proportionate; reuse source and requirement links rather than copying whole records. Each material finding needs an affected location or missing obligation, a concrete failure or consequence, and the correction or evidence needed to resolve it. Separate acceptance-blocking issues from optional suggestions; personal preference is not a blocker.

Return one outcome for the named snapshot and scope:

- **Acceptable:** the scoped obligations and required checks are supported, and no unresolved acceptance-blocking finding remains. List limits and any separately owned integration work; this is not permission to merge or a statement that the whole feature is delivered.
- **Changes needed:** identified defects, omissions or failed required checks need correction. Link each finding to the relevant obligation and assign its resolution to the worker or orchestrator.
- **Blocked:** missing inputs, required evidence, unavailable required checks or unresolved decisions prevent a supported acceptance conclusion. Include any defects already found and the smallest action that unblocks review.

When both defects and missing evidence exist, report both; use Blocked when the missing prerequisite prevents completing the assessment. Do not soften a required missing check into an optional follow-up. A proposed future analyser is not automatically a required gate: follow the actual agreement, describe the available assessment and retain its limitations.

State who performed the review and whether the reviewer authored the change. A fresh reviewer can provide independent review; a separate pass by the author is self-review. Neither label proves correctness. A delegated reviewer should receive the original obligations and actual change without the author's conclusions as an answer key. Delegate only when permitted by the user or project instructions.

## Preserve an interrupted review

When a review spans sessions, maintain partial progress only in its assigned report/checkpoint location: exact source snapshot, original obligations examined and remaining, evidence inspected, provisional findings, in-flight checks and next step. Label it **Review in progress** or **Interrupted**; absence of findings so far is not Acceptable. If no durable report location is available, return that limitation rather than implying the review can resume without rework.

A successor rereads current instructions and the original agreement, compares the recorded source state with the actual patch/base, and confirms review ownership with the coordinator. Carry forward supported findings, but reassess affected coverage when source or agreement changed. Unfinished checks and unexamined obligations remain incomplete. Reuse the saved coverage to finish the review without treating a partial record as a final verdict. Do not edit code or the shared roadmap to recover a review.

## Close the correction loop

Return findings to the orchestrator or requesting human; the worker makes corrections. On re-review, inspect the changed implementation and evidence, not just the response explaining the fix. Recheck affected obligations and connected behaviour, and state which findings are resolved or remain open. Do not repeat unrelated checks unless changed dependencies, the base or integration introduce a concrete risk.

Acceptance belongs to the reviewed snapshot. A changed patch, base, shared dependency or governing agreement requires an impact assessment and relevant re-review; do not carry approval forward silently. If required evidence stays unavailable or a decision is outside scope, stop with the blocker and next action rather than cycling indefinitely.

Only the orchestrator AI role may integrate or release, within explicitly granted user/project authority; authorised humans retain that ability. Reviewing, accepting a patch or possessing credentials grants no merge, push, release, deployment or external-comment permission. This skill returns its result; it does not automatically post comments, merge, release or mark delivery complete.
