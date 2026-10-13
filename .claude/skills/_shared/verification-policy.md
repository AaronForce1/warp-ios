# Behaviour-focused verification

Use this when designing verification, planning delivery, implementing or reviewing. Keep the project-specific verification contract in its existing conventions/checks record, otherwise `docs/conventions.md`; link it from the design and tasks. This is a small agreement about evidence, not a second specification or a new lifecycle stage.

## Select meaningful evidence

For web applications, centre acceptance on a small, dependable set of real-browser journeys exercising the running application: important successes, failures and recovery. Prefer Playwright for new browser-test setup unless an alternative is agreed. Preserve suitable existing tools. DOM-only component tests do not establish that the application works in a browser.

Add focused unit and integration tests where they provide clearer, faster evidence for business rules, boundary cases, service contracts or regressions. Choose the lowest useful level for each risk, while retaining whole-journey evidence for the promised user outcomes. Do not duplicate every scenario at every layer, generate exhaustive combinations without a concrete risk, or couple assertions to incidental internal structure. Do not remove useful existing tests just to match this preference. Test counts and arbitrary coverage targets are not success criteria; preserve explicitly configured gates unless changed under project authority.

Name which boundaries execute and which are replaced. Prefer controlled external services for repeatable browser tests that still exercise the real frontend and application server. Mocking the application's own route establishes a narrower UI check. Live-service tests separately establish provider compatibility and require suitable access and authority. A browser launch is startup evidence; a screenshot is visual evidence; neither alone proves a completed user journey. Missing credentials stay an explicit live-verification gap.

For UI changes, review the rendered result against the agreed flows and visual direction at relevant viewport sizes. Exercise keyboard interaction, focus, validation and relevant loading/error/empty states; include accessibility checks appropriate to the product. Link concise screenshots or traces and the inspected source state. Label agent visual inspection separately from actual human review. Static accessibility findings complement this work. Backend, CLI and Rust-only scopes use equivalent outcome-level checks at their real interface rather than adding an irrelevant browser suite.

## Configure tools to cover specific obligations

For each required check record: obligation/rule, code scope and exclusions, command or inspection method, tool/config version, what constitutes failure, evidence location and known limits. Name ownership of shared configuration and exception decisions. Required unavailable, crashed or incomplete checks remain unresolved and block acceptance; optional suggestions do not silently become new gates. Retain planned/configured/performed distinctions and recheck affected evidence after source, dependency or configuration changes.

The following tools are required wherever their stated scope applies. Design identifies applicability, Plan includes missing installation/configuration work, and delivery runs the configured gates during implementation and before acceptance/integration. Missing installation does not make a required tool optional. Use the project's package manager and pin versions. This policy does not itself install tools or change the saved evidence of an earlier trial.

| Required tool | Applicable scope and role |
|---|---|
| Language compiler/type checker and build | Type/compile/build correctness |
| [Biome](https://biomejs.dev/) | JavaScript/TypeScript formatting, lint and supported custom code-pattern rules |
| [dependency-cruiser](https://github.com/sverweij/dependency-cruiser) | JavaScript/TypeScript dependency boundaries derived from the agreed design |
| [Aislop](https://github.com/scanaislop/aislop) | Applicable code-quality/complexity and selected security findings; verify optional engine availability |
| [React Doctor](https://github.com/millionco/react-doctor) | React-specific quality findings where React is used |

An omission or replacement within an applicable scope needs explicit human agreement, recorded in the project check contract with the reason, affected assurance, alternative evidence and review/removal condition. Inapplicable tools need only a factual explanation (for example, no React code); an agent may not declare a tool inapplicable merely because it is inconvenient, unavailable or failing. Keep setup gaps visible and continue independent authorised work, but do not mark the affected delivery verified/complete until required checks pass or the human agrees an exception. For an existing project adopting this revision, reconcile gaps into its next plan/check contract; do not silently grandfather missing tools or rewrite historical passes as if the new checks ran.

Select one owner per overlapping rule so contradictory configurations and duplicate findings do not create noise; this does not permit dropping a required tool. Retain lockfiles/configuration. Assess security obligations explicitly, including secrets, vulnerable dependencies and relevant trust/permission boundaries; selected lint rules do not establish full security coverage. Rust needs its own compiler, tests, lint and architecture-analysis profile; use Aislop where supported, but do not imply TypeScript tools cover Rust. Any missing required capability remains unresolved. Avoid inventing numerical thresholds: justify and agree blocking rules and any metric gates. An aggregate score cannot cancel a blocking defect.

For architecture, trace generated rules to the approved model, identify unclassified/excluded source and check missing required elements/relationships as well as forbidden edges. Exercise important rules with representative allowed and deliberately violating examples. This need not become a large testing framework. Record parser support and analysis failures. Preserve the intended-versus-observed comparison and label unsupported claims as inspection or unresolved; an import graph does not establish runtime behaviour.

## Protect the meaning of a pass

Workers may propose legitimate test or configuration changes, but changes to assertions, exclusions, suppressions, rule severity or thresholds require explicit review against the original obligation. A worker cannot unilaterally waive a required check or weaken it to obtain a pass. Record an exception's scope, reason, authorised decision and review/removal condition. The orchestrator or an independent reviewer checks these changes; label any self-review limitation.

Before integration, reconcile the actual code snapshot, configured checks, review and source-linked evidence; verify the combined result after integration. Enforce worker merge/release restrictions and required checks through repository permissions where available, with honest disclosure where absent. Instructions and scores do not enforce credentials or prevent bypass. Use a bounded fix-and-recheck loop and escalate persistent failures or missing decisions rather than retrying unchanged work indefinitely.
