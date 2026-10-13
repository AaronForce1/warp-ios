# Delivery checkpoint: <bounded scope>

[Keep one current coordinator record linked from the roadmap, or use this section in the existing phase/task record. Workers own separate reports linked below. Update meaningful transitions; this is execution state, not a duplicate spec or task plan.]

## At a glance

[Keep this concise and current, following the skill's human-facing handoff guidance. Detailed recovery records follow below.]

- **Outcome:** <what is built or usable; local/committed/integrated/released state>
- **Verification:** <checks actually performed and important limits>
- **Remaining:** <material unfinished work or decisions; omit if none>
- **Next step:** <useful human action, or next work while the run continues>
- **Details:** <links to the roadmap, usage instructions or evidence as useful>

## Execution state

- **Run state:** In progress / Paused / Interrupted / Blocked / Complete
- **Delivery scope and agreement:** <requested product outcome and full plan/phase range; authoritative spec/design/plan; explicit exclusions or stop point>
- **Current assignment and remaining work:** <current phase/task within that scope; unfinished phases; the next ready work and its actual prerequisites>
- **Coordinator and authority:** <owner/run locator; actual grant source and limits; current human stop/pause instructions>
- **Last reconciled:** <when actual state was inspected; time alone never proves liveness>
- **Source:** <repository/worktree, branch, base/head, target and known dirty/untracked work>
- **Last evidenced milestone:** <result, source snapshot, checks/review and artifact links>
- **Next safe action:** <continue to the next in-scope assignment, reconcile state, or identify the specific blocker; a phase boundary alone is not a stop condition>

## Outstanding assignments

| Task / assignment reference | Owner and run locator | Work location / branch | Last observed state | Checkpoint / evidence | Next action or blocker |
|---|---|---|---|---|---|
| <stable task, linked scope and edit ownership> | <agent/role; locator only if available> | <recoverable local/shared location> | <active / finished / interrupted / cancelled / unknown; based on observation> | <worker-owned report, snapshot and verification> | <resume, wait, review, correct or reconcile ownership> |

## Pending operations

| Intended operation and target | Before state | Observed outcome / evidence | Reconciliation before retry |
|---|---|---|---|
| <dispatch, push, PR, merge or authorised release> | <known source/target and operation identity> | <not attempted / confirmed result / unknown> | <read-only lookup that can establish whether it happened; no blind duplicate> |

[Keep only unresolved operations and useful recovery references here. Record a confirmed outcome before removing the pending entry. If a mutation may have succeeded, inspect the actual system before retrying.]

## Recovery and verification limits

<Available storage and its lifetime; preservation of in-scope dirty/untracked work; active processes; inaccessible reports; superseded or incomplete checks/reviews; unresolved integration state. No credentials or secret payloads.>

On resume: read agreement/authority, inspect actual source and external state, reconcile workers and pending effects, confirm ownership, recheck affected evidence, then update the next safe action. A saved state does not restart an agent or grant permissions.
