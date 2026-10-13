# Worker handoff: <assigned scope>

- **Record state:** In progress / Interrupted / Final handoff. Partial work is not ready for review.
- **Handoff status:** Ready for review / Changes needed / Blocked; omit while still in progress.
- **Task and agreement:** <task IDs; links to authoritative requirements, design and plan>
- **Change location:** <checkout/branch, target branch, base and current head; retained dirty snapshot/diff if applicable>
- **Delivered change:** <concise outcome and important differences from the starting state>
- **Review artifact:** <actual PR or local diff and proposed PR summary>

## Evidence

| Requirement or design obligation | Command / method | Result and source snapshot | Evidence link and limits |
|---|---|---|---|
| <scoped promise> | <actual command or inspection; deterministic / AI / human> | <observed result; checked snapshot> | <artifact or source; mocked or unchecked boundaries> |

Include the observed-versus-intended architecture comparison where applicable. Record not-run required checks and invalidate results superseded by later changes. Do not populate this table with expected results as though observed.

## Remaining work and coordination

- **Unclosed requirements/findings:** <remaining scope, blocker or correction; none only when supported>
- **Shared records or interfaces:** <changes requested from their named owner>
- **Integration and combined verification:** <what the coordinator must still establish>
- **Risk / reversibility:** <material considerations for review; omit if immaterial>
- **Next action:** <review, correction or unblock decision and responsible role>

## Resume checkpoint — while work remains

- **Assignment / authority / owner:** <references to the actual grant and current assignment; worker/run locator>
- **Last evidenced milestone:** <what finished, checked source and accessible evidence>
- **Saved and active work:** <dirty/untracked work, durable recovery location, active command or operation and last observed state; exclude secrets>
- **Pending effect:** <intended target and known before/after state of a push/PR operation; unknown is not completed>
- **Next safe action:** <unfinished work or read-only reconciliation needed; confirm ownership before resuming edits>

Update this checkpoint during work. Inspect actual state before retrying a pending effect or reusing a result. Omit the section once no resumption remains necessary.
