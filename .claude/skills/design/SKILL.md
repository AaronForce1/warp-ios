---
name: design
description: Explore and document a software solution from agreed requirements, including architectural choices, C4 views with code-structure drill-down, interfaces, flows, and a verification approach. Use before implementation planning or when an existing design needs to change.
---

# Design

Help the human and agent choose an appropriate solution for the next bounded change. Design for clarity, testability and human verification: make responsibilities understandable, behaviour testable, and the intended structure inspectable before and after implementation. Explore the decisions that matter, explain the recommendation, and leave a design that another session can understand, plan and implement. Scale the work to the change; a small feature may need a short amendment to an existing design.

Read the relevant stage of the [bundled workflow](../_shared/development-workflow.md), alongside applicable project instructions. Project records use the project’s declared locations; bundled references resolve relative to this skill, not to the project’s docs folder.

## Establish the design problem

Read applicable project instructions, the current requirements, domain vocabulary, engineering conventions and relevant design decisions. For an existing system, inspect the affected code and tests before describing its structure. Distinguish observed behaviour, documented intent and proposed changes.

Use the feature map, when present, to locate all affected specifications and shared rules. Link each affected feature to the relevant design elements; features and architecture components need not map one-to-one. Keep shared architecture authoritative in the design rather than copying it into every feature spec. Reconcile cross-feature effects without reopening unrelated agreement.

Summarise the outcome to support, the constraints that shape it, and the decisions still needed. Reuse prior agreement. An upstream readiness label is useful context, not evidence that every premise is correct. If a discovered uncertainty changes required behaviour, return that point to requirements clarification. If it affects the chosen architecture, investigate or discuss it here. Continue independent design work while recording what depends on the unresolved question.

Use the project's record locations. Otherwise start with `docs/design.md`, linked from the relevant specification or roadmap. Respect the requested scope: discussion alone does not authorise file changes, and a design request does not itself authorise application implementation, commits or external actions.

## Explore the solution together

Start with the choices that have the greatest effect on the solution. Ask about relevant tradeoffs and explain them in terms of the user's outcome. Follow the consequences of answers rather than using a fixed questionnaire. Do not ask the user to select an architectural pattern without explaining why it would help.

For consequential choices, compare credible alternatives, including a simpler approach when one is viable. Describe what each gains, what it costs, and what future changes it makes easier or harder. Recommend an approach with reasons. More alternatives are useful only when they reveal a real tradeoff; routine reversible choices need little ceremony. For uncertainty spanning sessions, keep the decision map in the existing roadmap or phase record.

Use project standards first and choose the simplest architecture that satisfies the requirements and quality needs. Use SOLID and patterns such as clean or hexagonal architecture to reason about responsibilities and dependencies; a pattern name is not evidence of quality. Explain what the selected boundaries achieve and any deliberate coupling. Add layers or extension points only where they serve a current purpose.

Investigate external facts that materially influence a recommendation using relevant project evidence or primary sources. Keep a technical restriction distinct from a recommendation, report or assumption. An unknown does not make an approach impossible. Record useful evidence and its limits alongside the affected decision. A feasibility experiment can be proposed when documentation is insufficient; follow the user's authority for executing it.

## Select and record the technology stack

Apply [project preferences and supporting skills](../_shared/project-preferences.md). Reuse the existing preferences record, or capture relevant user choices from its template when useful. Apply defaults to new unconstrained choices; discuss conflicts with an existing stack and record agreed exceptions. Select available supporting skills for the platform and record their actual revisions or availability gaps. Use the agreed package manager in proposed setup commands.

Carry forward technology constraints already agreed in requirements or project standards. Identify the technology choices needed to make this design concrete: languages and runtimes, application frameworks, storage, external services, and build/test tooling where relevant. Recommend a stack in relation to the required behaviour, deployment environment, team conventions and architectural boundaries. For an existing system, reuse its stack unless a change has a clear benefit.

Record selected technologies, their roles and significant rationale in the design. Distinguish fixed constraints, chosen technologies and decisions that can wait. Include version or compatibility constraints when they affect the design; a complete dependency manifest is not needed at this stage. Reconcile stack choices and architecture as each develops.

Identify which language or framework readers the planned architecture checks will require. A selected stack is design context; it does not mean the analyser can enforce every technology choice. Record unsupported analysis explicitly rather than treating it as verified.

## Define the selected design

Develop enough detail to explain responsibilities and important interactions. Use the project's domain terms and stable references for design elements. Cover what the current scope needs:

- Components or modules, their responsibilities and ownership of data or state.
- Interfaces and dependencies: who may call whom, what crosses the boundary, and relevant error or ordering expectations.
- Important flows, including relevant user interactions, external integrations and failure paths. Explain where partial results, retries or concurrent work matter to the agreed behaviour.
- Trust boundaries and credential/data handling where relevant to the requirements.
- The expected source locations or project areas implementing these responsibilities, at a useful level of granularity.

Prefer interfaces that hide meaningful complexity and are natural to test. Demonstrate the consequential boundaries with a representative caller and a test scenario: what does the caller need to know, which module owns the policy, and how can important behaviour be exercised with controlled inputs or substitutes for external dependencies? Identify intentional framework or service coupling and its cost. Functions, modules, layers and ports/adapters are all viable; choose the amount of separation the system needs. Do not specify every internal function or implement the application to fill out the document.

For an existing system, show the affected current and target structure separately. Explain necessary coexistence, compatibility and temporary exceptions. Leave detailed phase and task sequencing to Plan, while recording constraints that sequencing must respect.

## Connect the model, diagrams and verification

### User interface agreement — when relevant

Use the selected UI skills to develop one coherent direction in the design: important user journeys, screen layouts or wireframes, component reuse, semantic visual tokens, responsive behaviour and relevant loading, empty, error and recovery states. Preserve existing brand/design-system choices. Keep screenshots or prototypes linked where useful, with the distinction between proposed and implemented views. Resolve conflicting specialist advice against project requirements and the human's agreement. Identify what rendered browser and interaction evidence will let the human review the result; diagrams and static checks alone do not verify UI quality.

### Authoritative design and navigation

The living Markdown design, including its diagram source and explicit rules, is the source of truth for the agreed architecture. Keep elements, relationships and important flows coherent using stable identifiers. Derived checker configuration and generated views must trace to that agreement; do not maintain a second, independently edited design. An existing external model may supply referenced detail, but identify its authority and reconcile it with the reviewed document.

Use C4 Context, Container, Component and Code views to support navigation from the system to the affected code structure. Keep Mermaid diagram source in Markdown; use suitable Mermaid class or flow diagrams for code structure and sequence diagrams for important flows. Record the configured renderer version and settings when available; flag rendering that has not been checked. Keep the technology stack consistent with the container and component descriptions.

For a small system, keep the views and rules in one document. As detail grows, link system, container and component records beneath the overview. A possible layout is `docs/design/systems/<system>/design.md`, then `containers/<container>/design.md` and `components/<component>.md`. Create folders only when useful. Parent records link to detailed views, child records identify their parent, and shared decisions have one authoritative location. All linked designs form the versioned agreement; Git retains its history.

### Required code-structure drill-down

For each component in the scope being designed or reviewed, provide or link a code-level diagram showing its proposed internal organisation before implementation. Include the modules, important types, interfaces or functions, and relationships needed to assess responsibilities and coupling. Reuse a sufficient existing view for an unchanged component. A simple component can have a very small view; exhaustive inventories of methods, variables or control paths are unnecessary. If an internal choice is deferred, identify it in the view and handoff rather than presenting it as settled.

Map stable design identifiers to existing or proposed source locations. Support TypeScript files, folders and packages, and Rust crates and modules, with language-appropriate types and interfaces; do not force both languages into an object-oriented class model. State what each relationship means, including whether it represents a source dependency or runtime interaction. Distinguish allowed, required and forbidden relationships, the default for unlisted dependencies, and any coverage exclusions or unresolved mappings. These records support review now; automated checking requires a defined parser and supported language analysis, whose availability must be stated.

Plan an observed code-structure view and an intended-versus-observed comparison for Verify and Review. Once code exists, derive observations from the actual source, using extraction tools where available and explicitly labelled agent inspection where needed. Record the source revision or working-tree snapshot, method, source links and coverage limitations. Preserve the intended view when producing observations; a generated diagram must not silently replace the agreement. With no implementation yet, mark the observed view as pending. Design need not implement the application or fabricate observations to complete this handoff.

### Verification approach

Apply the [verification policy](../_shared/verification-policy.md): centre web acceptance on critical real-browser journeys, supported by targeted unit/integration checks where they add value. Define which service boundaries are controlled and which require live evidence. Record the project check contract in existing conventions and link it here; missing agreed tooling becomes setup work in Plan, not an invented pass or a reason to implement during Design.

Link requirements and significant design rules to their intended verification:

- Behavioural tests for outcomes and relevant failure paths.
- Architecture checks for supported dependency or boundary rules.
- Other configured quality and security checks that apply.
- A separate AI or human review pass where judgment or unsupported analysis remains necessary, using the agreed design and actual source and citing the relevant elements and code.

Identify what each check would establish and what remains outside its coverage. Distinguish automatically checked results, AI-assessed findings, human review and unresolved claims; an AI assessment cannot override a configured check failure. Keep planned verification distinct from obtained evidence, and disclose unsupported analysis for each language. Reuse configured commands and rule identifiers; do not invent a passing result or treat architectural advice as a rule the tool already enforces. Diagrams explain structure and intended flows; behaviour requires separate test evidence.

Connect configured metrics and scores to the properties they measure, their scope and limitations. Before the analysis tool exists, record needed evidence as planned. A high score or an agent's assessment does not establish that humans can understand the design or that it fits the requirements. Improve the underlying design; do not introduce indirection, arbitrary splitting or weakened checks merely to improve a score.

## Record and discuss the proposal

Update the current design using the project's format or the [design template](assets/design.md). Link to requirements rather than duplicating the PRD. Keep ordinary decisions and rationale in the design; use separate ADRs only where significant tradeoffs and reversal costs make them useful. Update domain vocabulary when a design discussion genuinely clarifies its meaning.

Before presenting the recommendation, walk through an important success path and a material failure or boundary case. Follow the diagram links down to the code structure of the affected components and their source mappings. Reconcile the depicted dependencies with the boundary rules, and ensure responsibilities, interfaces and tests describe the same behaviour. Explain the walkthrough so a human can identify who owns each decision, what crosses a boundary and what evidence would reveal a mismatch; the review must not depend on access to the agent's reasoning. Human review remains possible even when the project delegates approval. Resolve issues that prevent selecting or planning the next scope; later reversible details may remain open with their consequences and when they must be decided. Do not turn this into a requirement for an exhaustive design of future work.

Recap the chosen approach, why it fits, significant alternatives and the decisions needing agreement. Apply existing confirmation or delegated design authority. Under the default workflow, obtain human agreement before implementation. If the response changes the proposal, reconcile the affected records and discuss its consequences. Do not record human approval for a decision made by the agent under delegation.

## Hand off to Plan

Keep one current status in the design and its roadmap entry where present:

- **Design in progress:** a material design choice, requirement change or feasibility question still prevents planning the next scope.
- **Awaiting agreement:** the proposal is ready for the applicable human decision.
- **Ready for Plan:** the selected approach is sufficiently defined for task breakdown and applicable agreement or delegation covers it. Deferred details and verification limitations remain visible.

The handoff identifies the authoritative requirements and design records, selected approach, component-to-code mappings and code-level views, important constraints on implementation, intended verification, and any deferred decisions with their consequences. Include the work needed to produce observed views and compare them to the agreed design during Verify and Review. Approval of a design does not imply implementation or successful checks.

Stop at this handoff when the request is limited to Design. Where a wider workflow is already authorised, continue within that scope. Later evidence can reopen the design or requirements; preserve unaffected decisions and make authorised changes visible in the current records.
