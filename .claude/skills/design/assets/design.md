# [Capability or bounded change] — solution design

**Design status:** [Design in progress / Awaiting agreement / Ready for Plan]
**Decision basis:** [Proposed, agreed by the human, or decided under applicable delegation.]
**Implementation:** [What exists now; what this design proposes.]
**Related records:** [Requirements, domain context, current design and applicable standards.]
**Design scope and navigation:** [System/container/component covered here; parent overview and child designs where split.]

[Adapt this template to the change. Keep useful sections, reuse existing records and remove these drafting notes from the output. Preserve the required code-structure drill-down, source mappings and comparison handoff. A small project can keep everything in this document; larger projects link system, container and component documents with shared stable IDs.]

## Design context

[Briefly state the outcome this design must support and the constraints that shape the approach. Link to the PRD for requirements and scope. For an existing system, distinguish observed structure from documented intent.]

## Options and selected approach

[For consequential choices, explain credible alternatives, the recommendation and its tradeoffs. Include a simpler option where viable. Preserve the reasons behind the choice and link consequential factual evidence. Routine decisions can be concise.]

| Decision | Selected approach and reason | Relevant alternative or limitation |
|---|---|---|
| [Decision] | [Choice, rationale and authority when material] | [Tradeoff] |

**Why these boundaries fit:** [Briefly demonstrate clarity, testability and human reviewability. Identify the owner of a meaningful policy, what its interface hides, and how a caller and a test would use it. Explain intentional coupling and why further separation would or would not help. Refer to the diagrams and test approach below; a pattern label or number of modules is not a quality argument.]

## Technology stack

[Carry forward existing constraints. Record the technologies needed to define this solution, including languages/runtimes, application frameworks, storage, external services and build/test tooling where relevant. Omit categories the system does not need. Link substantial tradeoffs to the decisions above.]

| Role | Technology and relevant compatibility constraints | Basis and reason |
|---|---|---|
| [Purpose in this system] | [Selected technology, existing constraint or unresolved choice] | [Why it fits; link any significant decision] |

**Architecture-analysis support:** [Required language/framework readers, known available support and relevant limitations. Selecting a technology does not establish that the analyser supports it.]

## Structure and responsibilities

[For UI scope, include or link one agreed UI direction: key journeys, layouts/wireframes, reusable components and visual tokens, responsive behaviour and relevant loading/error/empty states. Link project preferences, selected supporting skills and agreed exceptions. State how the rendered result and interactions will be reviewed. Omit for non-UI scope.]

**Design authority:** [This Markdown design and its linked design documents contain the agreed architecture, Mermaid source and rules. Identify any referenced authoritative detail. Derived configurations and views trace back here.]

**Automated analysis:** [Configured parser/model adapter and language readers, if any; otherwise state that automated conformance is unavailable. These tables are review records until a supported schema and implementation are defined.]

| Element ID and C4 level | Responsibility and owned state/data | Source mapping and status | Detailed view |
|---|---|---|---|
| [Stable ID, name and parent] | [Purpose] | [Existing/proposed TypeScript path/package or Rust crate/module; external elements have no local source] | [Section or child design containing the component's code structure] |

| Relationship ID | From → to | Meaning | Constraint |
|---|---|---|---|
| [Stable ID] | [Element IDs] | [Source dependency or runtime interaction; interface/data crossing] | [Allowed, required or forbidden; applicable scope and rationale] |

**Mapping and boundary coverage:** [Code areas covered, exclusions, unresolved mappings, and treatment of unlisted dependencies. State supported analysis and gaps. A runtime interaction does not itself imply a source import.]

### C4 overview and component views

[Include Mermaid C4 Context, Container and Component views for the relevant scope, or link existing authoritative views. Use the same IDs as the records above. Label intended structure. Include navigation to each affected component's code-level view, within this document or in a linked child design. Record renderer version/configuration and whether rendering has been checked.]

### Code structure — required drill-down

[For every component in the design/review scope, include or link a focused Mermaid class or flow diagram of its intended internal structure. Show the modules, important types/interfaces/functions and their relationships needed to review responsibility and coupling. Use language-appropriate notation for TypeScript and Rust. A simple component can have a small diagram; reuse sufficient existing views for unchanged components. Identify deferred choices visibly. Do not inventory every method, variable or control path.]

| Code element ID | Role and relationships | Existing or proposed source location |
|---|---|---|
| [ID used in the diagram, linked to its parent component] | [Responsibility, relevant interface and dependency] | [File/module/symbol reference; clearly mark locations that do not exist yet] |

### Observed structure and comparison handoff

**Observed view status:** [Pending implementation / available for the inspected source snapshot / incomplete with stated gaps.]

[During Design, specify how Verify and Review will obtain the observed code-level views, map them to the intended elements and report differences. Once implementation exists, retain the intended views and add or link observations derived from the actual source. Record source revision or working-tree snapshot, extraction tool or agent-inspection method, source links and coverage limits. Separate AI interpretations from mechanically extracted facts. Do not draw a proposed structure again and label it observed.]

[The comparison reports matching structure, missing required elements/relationships, boundary violations, extra or unmapped code, and unresolved observations within the declared scope. Unsupported analysis is a visible limitation. Any change to agreed intent follows project authority; the observed view does not replace it automatically.]

## Important flows

[For each important flow, link its requirement, identify the trigger, participating elements, meaningful state changes and outcome. Include a sequence/activity diagram or another suitable flow view. Describe relevant failure or incomplete-result behaviour and recovery boundaries. Reuse requirements rather than redefining them.]

## Interfaces, data and trust boundaries

[Describe the contracts and data/state relationships needed to plan the work. Include relevant validation, ownership, errors and ordering expectations. Explain relevant sensitive-data and credential boundaries. Link substantial interface contracts separately only when useful.]

## Verification approach

**Project check contract:** [Link existing conventions/checks record: required tools and versions, scope/exclusions, failure criteria, missing setup, evidence and exception ownership. Do not invent configured gates.]

**Behaviour and UI evidence:** [Important real-browser journeys for web scope, preferably Playwright for new setup unless another approach is agreed; selected unit/integration checks for distinct risks. Name mocked boundaries versus live services, viewport/keyboard/visual review and required access. Use equivalent interface-level checks for non-web work. Avoid arbitrary test-count or coverage goals.]

| Requirement or design rule | Verification method | Availability, evidence and limits |
|---|---|---|
| [Existing requirement/rule reference] | [Automated check/test, separate AI assessment or human review] | [Planned/configured/performed; evidence and code/design references when performed; unresolved scope] |

[Include the intended-versus-observed structure comparison, important success and failure tests, and applicable project quality/security checks. Report automatically checked, AI-assessed, human-reviewed and unresolved claims distinctly; AI judgment cannot override a configured check failure. A planned check is not a passing result. A structural match or diagram does not establish behavioural correctness.]

[For configured metrics/scores, identify the property measured and coverage limits; leave unavailable tooling explicitly planned. Scores support specific claims and do not replace human assessment of clarity or suitability. Do not invent thresholds.]

**Human review walkthrough:** [Use an important success and failure/boundary case to trace requirements through the relevant diagrams, policy owners, interfaces and proposed source locations. Make the permitted dependencies and intended test evidence understandable without the authoring agent present. Identify what a later intended-versus-observed comparison would reveal. Reuse the flow descriptions rather than copying them. Record actual human agreement separately from making the design reviewable.]

## Existing-system transition

[Include when relevant: affected current and target structure, behaviour to preserve or intentionally change, coexistence constraints and temporary exceptions with their intended resolution. Detailed delivery phases and tasks belong in Plan.]

## Risks and remaining decisions

[Record meaningful risks, mitigations, consequential assumptions and outstanding decisions. Distinguish what prevents planning this scope from details that can safely be decided later. A deferred choice needs its consequence and the point at which it must be settled; avoid generic lists of hypothetical risks.]

## Plan handoff

[Use the same status as the header and roadmap. Identify the authoritative design documents, their agreement/delegation basis, code-level views and mappings, constraints on task sequencing, intended verification and any deferred choices. Include the future work to produce observed structure and compare it with the agreed design. Record requirements changes that need clarification. Design completion does not require unbuilt code to have an observed view and does not mark implementation complete or checks passed.]
