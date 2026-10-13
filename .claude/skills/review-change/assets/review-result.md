# Review: <change or task scope>

- **Review state:** In progress / Interrupted / Final result
- **Outcome:** Acceptable / Changes needed / Blocked; omit until a scoped conclusion is supported.
- **Scope:** <task IDs, authoritative requirements/design/plan links, exclusions>
- **Snapshot:** <actual base/head; include saved dirty snapshot identity when relevant>
- **Reviewer:** <role; independent reviewer or self-review>

## Findings

For each material finding: identify whether it blocks acceptance, link the affected source or missing obligation, describe a concrete consequence, and state the required correction/evidence and responsible role. Keep optional suggestions separate. If none are found, say so within the reviewed scope and limits.

## Obligations and evidence

| Material obligation | Implementation/source | Evidence and actual result | Method and limits |
|---|---|---|---|
| <requirement, design boundary or applicable check> | <link, or missing> | <examined log/test/comparison, snapshot and outcome> | <automated / AI / human / unresolved; relevant mocks, gaps> |

Group related obligations only where their closure remains clear. Include relevant architecture comparison and integration evidence; link existing records rather than duplicate them. Required missing checks remain unresolved.

## Handoff

- **Corrections or unblock action:** <owner and concrete next step, or none>
- **Integration still required:** <combined verification / dependencies / owner, or not applicable>
- **Review limits:** <unexamined areas and their effect on the conclusion>
- **Re-review:** <resolved/remaining prior findings and scope rechecked, when applicable>

This result applies to the identified snapshot and scope. Changes require an impact assessment and applicable re-review. Acceptance does not grant merge or release authority or mark the feature delivered.

## Resume checkpoint — for an unfinished review

<Assigned reviewer/owner and report location; last inspected source; obligations covered and remaining; provisional findings and evidence pointers; active checks with observed state; next step. Reconcile changes to source/agreement and ownership before continuing. A partial review is not an acceptance verdict.>
