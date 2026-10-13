# [Capability or bounded change]

**Understand status:** [Clarification ongoing / Awaiting confirmation / Ready for Design — select one current state.]
**Agreement:** [In discussion, agreed, or decided under applicable delegation; retain only what is supported. Keep provisional while requirement-level assumptions remain unresolved.]
**Delivery:** [Describe what exists on this branch and what is still planned.]
**Feature reference:** [Existing stable capability reference when used; preserve requirement IDs across moves.]
**Related records:** [Feature map, shared glossary/rules, affected neighbouring specs, roadmap/phase, design, or decision records.]

## Problem and intended outcome

[Who is affected, what problem they face, and what useful outcome this change should achieve.]

## Scope

- Included: [Bounded behaviour or capability.]
- Excluded: [Explicit exclusions and deferred scope.]

## Starting point and proposed change

[For existing systems: documented contract, relevant implementation observations and evidence, and intended changes. For a new system: make the absence of an implementation clear. Do not present a proposal as delivered behaviour.]

## Requirements and acceptance examples

### [Stable requirement reference]: [Short title]

[Required observable behaviour, preserving supplied conditions and limits.]

- Example: Given [relevant state], when [event], then [observable outcome].
- Relevant failure or boundary case: [Condition and expected response, where material.]

[Repeat for independently meaningful obligations. Reuse existing project identifiers and scenario conventions. Check that definitions and rules imply the same results. Include relevant combined success, empty and failure examples, and the visible outcome when source information or results are incomplete.]

## Constraints and dependencies

[Applicable project standards, external contracts, supplied technology constraints, and dependencies that affect the requested behaviour. Link to shared standards instead of duplicating them.]

## Decisions and rationale

[Preserve useful reasons for agreed choices next to the relevant requirements, or summarise them here without duplicating the requirements. Distinguish verified facts, user decisions and delegated decisions. Link evidence for consequential external limitations and any warranted ADRs. Ordinary decisions need no separate ADR. Omit this section when rationale is already captured where it belongs.]

## Unresolved requirements

[During clarification, list unanswered requirements and assumptions, their effects, and the next decision or evidence needed, including dependencies that prevent an answer yet. Partial answers leave their unanswered parts open. Continue the interview to resolve them. Transfer settled answers into requirements or constraints and remove them here. For a ready handoff, state that none remain within the agreed scope, or omit this section; do not retain silent assumptions. Explicitly deferred features belong in excluded/deferred scope.]

## Design handoff questions

[Implementation choices about how to meet settled requirements may remain here. A choice that changes expected behaviour, scope, or acceptance conditions must return to Understand. Omit this section when unnecessary.]

## Readiness review

[Before the recap, derive the review entries from material claims in the saved requirements, examples, constraints, glossary and rationale, including implied guarantees. A claim is material when its truth or meaning affects the outcome, acceptance or feasibility. Use existing references; group claims only if the same evidence and challenge cover each. Reuse existing examples and sources rather than duplicating them.]

| Claim and record references | Supporting evidence or decision, and limits | Concrete challenge and result | Status and remaining gap |
|---|---|---|---|
| [One material promise, definition, relationship or tightly coupled rule; link its requirements and other affected records.] | [Link support for this exact claim and distinguish documented fact, scoped observation, report, inference or agreed choice. State applicable conditions and uncertainty. An evidence caveat does not establish the claim.] | [Concrete inputs, expected result and actual conclusion. For consequential impossibility/necessity claims, record the contrary evidence sought and assessed. For numerical assurances, include units, assumptions and calculation. A hypothetical case is not proof of external behaviour.] | [Open until checked and supported; Satisfied only for the supported scope. State the gap and next evidence or decision needed. A recommendation or default is not proof of a technical restriction.] |

**Coverage:** [Identify the records and requirement references examined. Check that each material claim maps to an entry, including failure promises and consequential explanations in glossary/rationale. Add omitted claims as Open. Name remaining gaps; a category-wide pass or source list alone does not establish coverage.]

[Open or unchecked claims keep Clarification ongoing. Resolve the evidence gap or behavioural choice, update all affected records and recheck dependent claims. Confirmation does not establish a technical fact. Preserve evidence limits in the recap and handoff; reports and inferences must not become verified facts in the summary. After changes, reassess the current saved records before declaring readiness.]

## Understand handoff

[Use the same current status as the header and roadmap and refer to the Readiness review. Clarification ongoing: an unchecked or Open claim, requirement or assumption still needs evidence or a decision. Awaiting confirmation: the review is satisfied, the recap is presented, and only confirmation remains. Ready for Design: the review covers and supports the material claims in the current saved records with no unchecked or Open claims, records agree, and the current recap is confirmed or covered by applicable delegation. After confirmation or a correction, check coverage and affected evidence before updating status. Name genuine Design questions and affected records. Refer only to accessible evidence and decisions. Do not combine states into "ready, pending confirmation," mark implementation complete, or claim unrun checks passed.]
