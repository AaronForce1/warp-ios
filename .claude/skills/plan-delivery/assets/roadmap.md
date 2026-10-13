# [Project] — roadmap

**Current planning scope:** [Bounded change or phase.]
**Planning coverage:** [Task breakdowns for every phase in that requested scope, or the specific remaining planning gaps and their justified deferrals.]
**Planning status:** [Planning in progress / Awaiting agreement / Ready for implementation; applies only to the named scope.]
**Planning basis:** [Links to current requirements, design and relevant standards; revision or description of uncommitted inputs.]
**Agreement:** [Existing authority and any pending decision; do not imply approval from this template.]

[Reuse the project's roadmap. Keep one concise overview; add phase files only when their detail helps. Remove drafting notes and unused sections. Planned work remains distinct from delivered behaviour.]

## Direction and current state

[Intended outcome, relevant implemented behaviour, and what remains. Link the specification and design for their authoritative detail.]

## Build progress

**Status key:** ⬜ Planned · 🟡 In progress · 🚧 Blocked · 🔎 Verifying/reviewing · ✅ Complete. Deferred and Cancelled remain separately labelled.
**Coordination:** [Single agent or coordinating role; unassigned until known. For parallel work, the coordinator maintains this overview from worker reports and integration evidence.]
**Feature map:** [Link when present. Omit if unnecessary.]

[Keep this overview across feature cycles. Preserve unrelated work and supported completion history. Use rows at feature/phase granularity appropriate to the build; link detailed task records rather than copying them. Green ticks require scoped acceptance, applicable checks/review and integration evidence; planning agreement is not delivery.]

## Phases

| Feature / phase and outcome | Spec / design | Owner | Dependencies / blocker | Delivery status | Detail and exit evidence |
|---|---|---|---|---|---|
| [Stable ID: observable result] | [Links; full or partial contribution] | [Agent/role or unassigned] | [Actual prerequisites; reason if blocked] | [Icon + text from key, or Deferred / Cancelled] | [Task/phase link and planned or obtained evidence; integration if partial] |

[Every phase in the requested scope needs reviewable tasks, dependencies and completion evidence, inline or linked. The next phase may be finer-grained. Outline-only work needs an explicit user choice or a specific unresolved decision, with the affected scope, reason and resolution point recorded. Unfinished predecessor work does not itself prevent planning later phases. Preserve completed results with evidence; a completed plan does not mean a delivered phase.]

## Next scope

**Next task:** [Stable reference and intended result.]
**Prerequisites:** [Available now, planned work, or unresolved blocker.]
**Continuation:** [Requested scope and next stage; readiness is not permission to implement.]

[For small work, include tasks here using the compact task block below. For larger work, link the phase plan and omit this duplicate detail.]

### [Task ID] — [Result]

- [ ] [Deliverable; remain unchecked until completion is evidenced.]
- **Supports / changes:** [Requirement and design links; affected areas and limits.]
- **Owner / coordination:** [Agent/role or unassigned. For parallel work: exclusive edit scope, shared-file/contract owner or edit sequence, result handoff and integration owner/task. Omit extra coordination detail for simple solo work.]
- **Depends on:** [Task references, verification setup and blocking decisions; distinguish prerequisites to start and finish when useful.]
- **Acceptance and verification:** [Observable result and evidence at its responsible boundary; controlled scenarios versus live checks, availability and limits. State partial scope and later closing work when applicable.]
- **Delivery status / evidence:** [Planned initially; actual results and applicable review only when obtained.]

## Deferred scope and decisions

[Only relevant pending scope, decisions and blocked work; why deferred, where owned, and when needed. A decision blocking the next task prevents readiness for that task; a later decision need not block independent work.]

## Planning review and handoff

**Review method and basis:** [Fresh reviewer or separate self-review; source records and saved plan state reviewed. Do not describe self-review as independent.]

[Derive the material obligations from the original requirements, design, project instructions and workflow before assessing the plan's claims. Include required verification, architecture comparison, documentation and completion work. Link the resulting closure reviews in phase exit sections; record any unassigned obligations here so omitted work stays visible. For a small plan kept here, use the table below; otherwise omit the duplicate table. A category-wide assertion that coverage was reviewed is insufficient.]

| Observable outcome / reference | Closing tasks and planned acceptance scenario | Evidence boundary and limits | Counterexample considered | Resolution and coverage |
|---|---|---|---|---|
| [Obligation and original source link] | [Tasks, or missing assignment; setup/action/expected result or inspection] | [Where observed; relevant behaviour bypassed by mocks or otherwise unchecked] | [Concrete way the checks could pass while the result is wrong] | [Correction reference or how evidence covers the case; fully planned / partial / missing / justified deferral with remaining work and resolution point] |

[Summarise material findings, corrections with task/section references, and remaining affected scope. Recheck the saved corrections and their dependencies; a finding acknowledged only in this summary remains open. Reconcile full/partial claims across tasks, phase exits and this roadmap. Confirm every phase has a breakdown or justified gap and prerequisites match setup and sequence. For inline plans, name required observed-view/comparison artifacts, source navigation and limits. State whole-request coverage separately from the next executable task. Missing required work or planned evidence prevents a full-coverage claim, while independent tasks may be ready. This review does not test an implementation.]
