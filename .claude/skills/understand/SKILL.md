---
name: understand
description: Interview the user iteratively to resolve a software idea, feature change, or refactoring request into agreed living requirements, acceptance examples, shared vocabulary, and a handoff to solution design. Use when intent or scope needs establishing before design and implementation.
---

# Understand

Reach a shared understanding of the requirements for the next bounded piece of work through an iterative interview. Preserve decisions in the project's current repository records as the discussion develops so another person or agent can resume without the original conversation. Producing those records does not by itself complete Understand.

Read the relevant stage of the [bundled workflow](../_shared/development-workflow.md), alongside applicable project instructions. Project records use the project’s declared locations; bundled references resolve relative to this skill, not to the project’s docs folder.

## Establish the starting point

Read existing technology preferences using [project preferences](../_shared/project-preferences.md). Retain user-supplied defaults separately from product requirements; clarify only constraints that affect intent or scope here and hand solution choices to Design. Missing preferences or supporting UI skills do not block discovery.

Read the project-root `AGENTS.md` when present, along with the request, other applicable project instructions, relevant current specifications, domain vocabulary, roadmap, and decisions already made. For an existing system, inspect enough relevant code and tests to distinguish documented intent, observed implementation, and requested change. State when evidence is unavailable; do not infer successful behaviour just from a test's existence.

Use document locations declared by project instructions; otherwise reuse existing records and naming conventions. When locations are not yet established, keep new records together under `docs/`. Create only the records needed for the request. Scale the investigation to the change: a small adjustment should not trigger a new project-wide discovery exercise. For a refactor, identify behaviour to preserve and any intentionally changed behaviour.

Respect the scope of the current request. Advice or discussion alone does not authorise repository edits, issue publication, or implementation. Where documentation work is authorised, maintain its records during the discussion. Otherwise present the proposed content for the user.

## Locate the affected features

Before editing requirements, identify the capabilities affected by the request and where their current agreement lives. Reuse the feature map when present. Update an existing feature specification for changed behaviour; give a substantial new capability its own living specification. Organise around capabilities, including background and cross-cutting behaviour, rather than assuming each screen or route is a feature.

When a single specification becomes difficult to navigate, split the affected material into linked feature records instead of appending another unrelated section. Preserve requirement identifiers, agreement, pending changes and useful rationale; update incoming links and leave each requirement with one authoritative home. Do not reorganise unrelated records just to impose a new layout.

Use project conventions. Otherwise a lightweight default is `docs/specs/README.md` as the feature map and `docs/specs/<feature>.md` for substantial capabilities, with capability-group folders only as needed. The map links feature purpose, specification and relevant design; the roadmap owns delivery progress. A small project can retain one spec. Use the [feature-map template](assets/feature-map.md) only when navigation benefits from it. Keep shared rules and vocabulary in one place and reference them from affected features. A change spanning features must identify all affected records and reconcile their shared behaviour.

## Interview through the decisions

Establish the problem, affected users, intended outcome and bounded scope. Track what is settled, what is unresolved, and which decisions or facts each open question depends on. Use the conversation and current records; a separate decision-tracking document is unnecessary.

Work in rounds:

1. **Ask what can be decided now.** Select a coherent group of unresolved questions whose prerequisites are settled. Number them for easy replies. Offer a recommendation with its reason and tradeoff where useful, clearly separate from an agreed decision. A question must not assume the answer to another unanswered question in the same round. Wait for the user's answers before resolving dependent questions, unless that decision is already delegated.
2. **Interpret the answers.** Carry forward earlier agreement. If an answer introduces scope, answers only part of a question, conflicts with another decision, or admits materially different interpretations, identify that explicitly. Keep the original unanswered part open. A short answer does not authorise filling in a consequential missing choice.
3. **Follow the consequences.** Incorporate settled answers into the records and remove them from the unresolved list. Identify the new choices, contradictions and factual dependencies those answers expose. Ask the next round based on these consequences, rather than moving to document production because the first questions were answered.
4. **Challenge apparent closure.** When no known requirement questions remain, reconcile the written draft and run the readiness review below against those saved records. A gap reopens the relevant discussion. Once the review is satisfied, recap the outcome, scope, exclusions, decisions and acceptance examples, and obtain the required confirmation or apply existing delegation.

Continue until the requested scope is understood or the user pauses. No fixed round count or question quota applies. An explicitly excluded feature need not be designed now; an unanswered requirement within scope keeps the handoff incomplete. Reuse decisions and confirmations already given for the current agreement. Under delegated authority, distinguish agent decisions from human confirmation; silence is neither. Preserve agreed quantities, limits and exclusions; do not invent targets or preferences to fill a template.

For each capability, use its user, trigger, inputs, result, state, boundaries, failures and dependencies to find missing behaviour. These are prompts for reasoning, not a questionnaire to recite. Challenge a proposed solution when it fails the outcome or adds unnecessary work. Preserve supplied constraints; defer undecided implementation choices to Design. Choices that affect observable behaviour or acceptance stay in Understand. Required project checks remain requirements, regardless of implementation autonomy.

Investigate facts using project evidence or authoritative sources before relying on them in recommendations. Distinguish a verified limitation from an estimate or assumption. When evidence is unavailable, keep its consequential effect open; continue independent questions. Ask the user to decide desired behaviour and tradeoffs, not to confirm an unverified API capability or implementation-cost claim as fact.

## Clarify domain language throughout

Develop the vocabulary during the interview. For an overloaded or vague term, propose a precise meaning and use a concrete case where competing meanings would change the result. Check relationships, identity and counting rules, boundaries and state changes where they matter. A plausible interpretation is still an assumption until supported by the answers, evidence or delegated authority.

Record agreed meanings in context and update the affected requirements and examples together. New terminology questions can reopen apparently settled requirements. Keep domain meanings separate from code types, module structure and implementation data flow, which belong in Design.

## Review the saved specification before readiness

This is a distinct step after writing or reconciling the draft and before the final recap. Read the saved specification, context and roadmap together: review what they actually promise, including details introduced while writing. Do not infer that the review passed because the interview ended or the user agreed.

Build the **Readiness review** from the saved claims, not from a list of review categories. Scan each in-scope requirement, acceptance example, constraint, glossary definition, rationale and Design deferral for claims whose truth or meaning affects the outcome, acceptance or feasibility. Include implied guarantees and causal explanations, not just explicit requirements. Use their existing identifiers or section links; a separate inventory document is unnecessary.

Record one concise entry per material claim or tightly coupled rule, with its record references, supporting evidence or decision, concrete challenge and result, and **Open** or **Satisfied** status. Group claims only when the same evidence and challenge cover them all. Unchecked, unsupported or contradicted claims start **Open**. A category-wide pass cannot stand in for missing entries. Reuse existing examples and evidence to keep this proportionate.

For each entry, apply the checks its claim needs:

1. **Match evidence to the exact promise.** Link the source and distinguish documented support, scoped observation, third-party report and inference. Prefer current primary documentation, maintained implementation evidence or the relevant contract. Explain what the evidence establishes under the applicable conditions, including negative outcomes and information a dependency may withhold. A source confirming one capability does not establish a related guarantee; a hypothetical case does not establish actual external behaviour. Multiple reports of a failure do not establish a universal limitation, and acknowledging weak evidence does not make the claim Satisfied. Narrow the claim to what is supported or keep its consequential uncertainty Open.

   Before a claim of impossibility or necessity changes scope or rules out the user's chosen approach, actively seek contrary evidence in primary documentation or maintained implementations. Record what was checked and whether it supports the same endpoint, version or environment where those conditions matter. Distinguish a recommendation or default setting from a technical restriction. Failure to find support is not proof of impossibility. If the premise remains unestablished, explain that uncertainty; an alternative may be recommended on its own merits, but must not be presented as forced by an unverified fact. This is targeted research, not implementation or an unauthorised live test.
2. **Try to falsify the rule or explanation.** Derive acceptance results from their actual inputs and definitions, then use a plausible contrasting case that could make the claim false or expose two different interpretations. Record the inputs, expected outcome and why the rule survives or needs correction. Check consequential relationships between events, states and measurements rather than treating them as interchangeable. For flows with multiple sources or stages, include relevant empty, incomplete and failed outcomes, including an earlier success followed by failure. Naming a case or repeating the requirement is not a challenge result. Cover material cases, not every theoretical combination.
3. **Check quantitative assurances.** When a number justifies feasibility, capacity, cost or an acceptance claim, record the inputs, units, assumptions and calculation. Distinguish quantities such as records, requests and bytes; account for any extra work needed to filter, paginate or establish exact totals. Check the arithmetic and whether the assumptions are established. An output cap or a label such as on-demand does not by itself bound upstream work or usage frequency. Preserve user-chosen limits as decisions; they do not need invented technical justification. Leave implementation estimates to Design when readiness does not depend on them, and remove unsupported assurances from the agreement.
4. **Check the agreement and its recording.** Match intended behaviour to the user's answers or applicable delegation; these establish choices, not external facts. Reconcile missing answers, inferred choices, glossary meanings, rationale, examples and proposed-versus-delivered claims. Questions whose answers change acceptance stay in Understand. Genuine choices about how to implement a settled outcome may remain in Design.

Before marking the review satisfied, scan the saved records again for omitted material claims and changes made during review. Each must link to a supported entry; an omitted check is still Open. State the records and requirement references covered, and name remaining gaps. Preserve evidence limits in the recap and handoff: reported or inferred findings must not become verified facts in the summary. Do not infer complete coverage from a full-looking table or a list of sources.

Any **Open** claim keeps **Clarification ongoing**, even if the user has confirmed the recap. Resolve factual gaps through evidence, explain constraints that affect the requested outcome, and ask focused questions only for undecided behaviour. Apply corrections to every affected record, including glossary and rationale, then recheck the claim and its dependants. Preserve settled choices and unaffected evidence. Do not clear a finding merely by removing its review entry, relabelling it as a Design question, or citing user confirmation as proof of feasibility.

When no material gap remains, present the recap and obtain any required confirmation. If the response introduces a change, reconcile and review its effects before advancing. Confirmation establishes agreement; the recorded review separately establishes the basis for readiness. Neither an empty unresolved list nor a confirmation alone is enough.

## Maintain the living records

- **Specification:** record the desired behaviour, acceptance examples, constraints, exclusions, decisions with useful rationale, assumptions, and remaining questions. The saved spec includes corrections made after a conversational recap; the transcript or glossary cannot substitute for it. Preserve existing requirement identifiers; add stable references when needed for downstream design and tests. Label proposed changes and delivery status separately from agreement to the requirements.
- **Domain glossary:** capture only useful domain terms and their agreed meanings. Reuse existing terms; explain conflicting meanings when necessary. Create a glossary only when useful; default to `docs/GLOSSARY.md` for new records, while reusing an existing vocabulary file unless migration is requested. Keep detailed requirements and implementation plans in their own records.
- **Feature map:** when used, maintain links to each affected capability and its authoritative specification and design. Keep delivery status in the roadmap rather than maintaining a second progress table.
- **Roadmap or phase document:** keep a concise reference to the requested outcome and its actual status. Use the existing single roadmap. A planning result does not complete an implementation task, and a small change does not require a separate phase file.
- **Decision rationale:** keep ordinary decisions and factual constraints with the relevant spec requirement. Use an ADR when a consequential choice has meaningful reversal cost and its alternatives or non-obvious rationale would otherwise be lost. A surprising fact or error message alone does not require one. Describe constraints and future obligations accurately; recording a decision does not mean its implementation, documentation or verification is complete.

Use the project's existing formats. If a suitable format is absent, adapt the [specification template](assets/specification.md) and, when needed, the [glossary template](assets/glossary.md). Omit irrelevant sections rather than creating empty paperwork. Templates are output aids, not additional prerequisites.

For existing behaviour, proposed amendments must remain distinguishable from what the current branch implements. Preserve the current contract while recording intended changes. A discrepancy between code and spec may be a defect or a reason to reconsider intent; changing the agreement requires applicable authority, not automatic acceptance of the code.

Authoritative records belong in the repository alongside the code. Updating files does not imply committing, publishing, or opening issues. Use the project's authorised delivery process for those actions. Git retains superseded versions; avoid creating completed-change archive folders or duplicate specifications in a tracker.

## Support larger efforts when needed

When uncertainty spans sessions, use Wayfinder-style decision mapping inside the relevant roadmap or phase document. Record unresolved decisions, their dependencies, the research needed, and the next useful decision to resolve. Keep this proportionate; no external skill, tracker, or additional document layer is required.

As decisions resolve, carry their substance into the current specification or design. Do not leave governing requirements only in discussion notes. Preserve unresolved dependencies for the next session without prematurely specifying every future phase.

## Hand off to Design

Before reporting readiness, check that the next scope has:

- A clear problem, affected users, and intended outcome.
- Concrete behavioural requirements and acceptance examples, including material failure cases.
- Relevant constraints, exclusions, and consistent terminology.
- A recorded readiness review covering the material claims in the current records with supporting evidence and concrete challenges, no unchecked or Open claims, and no unresolved requirement-level assumptions or unanswered requirements within that scope.
- A shared-understanding recap confirmed by the user, already covered by explicit agreement, or settled under applicable delegated authority.
- Accessible current records with proposed work and implementation status distinguished.

Check consistency across the specification, domain context, and roadmap: no item may be treated as agreed in one place and unresolved elsewhere. Keep readiness and agreement status provisional until the clarification loop is closed.

Use one current Understand status consistently in the specification, roadmap, and conversational handoff:

- **Clarification ongoing:** a requirement, assumption, fact affecting the scoped requirements, or consequential inconsistency still needs resolution. If work is paused, preserve the outstanding question and resume point under this status.
- **Awaiting confirmation:** the recorded readiness review is satisfied and the recap has been presented; only confirmation remains. A question that still changes required behaviour belongs in Clarification ongoing.
- **Ready for Design:** the recorded readiness review covers and supports the material claims in the current saved records with no unchecked or Open claims, requirements within scope are settled, records agree, and the current recap is confirmed or covered by applicable delegated authority.

Use these states directly; do not combine them into "ready, pending confirmation." After confirmation or a correction, update the affected records and check that the readiness evidence still supports them before reporting the resulting status. A positive answer must not trigger a status-only promotion while a material gap remains. References to decisions or recaps must identify content that actually exists and remains accessible.

Questions properly belonging to Design may remain open in a separate handoff section. Link the records changed and identify the next bounded responsibility or the decision preventing readiness.

Readiness is an assessment of the requirements, not proof that code exists, tests pass, or architecture conforms. Proceed to Design only when that continuation is within the user's requested scope and applicable project instructions.
