# Development workflow skill bundle



This bundle supplies Understand, Design, Plan Delivery, Implement, Review Change and Orchestrate Delivery. Shared workflow and delivery instructions live in `_shared/`; each skill carries its own output templates.

## Install into another project

Copy the six skill directories **and `_shared/` together** into the target assistant's supported skill directory, preserving their sibling layout. For the current Claude Code setup, that directory is `.claude/skills/`. Copying a single skill folder alone omits its shared references. The proposed npm/npx installer is not implemented yet.

Add links to the bundled workflow and delivery contract in the project's existing agent instructions, using the actual installation location. Merge those pointers with existing conventions; do not replace project instructions or copy Repohood Watch's product records. Ensure the chosen assistant loads those project instructions using its supported mechanism.

- [Workflow](./_shared/development-workflow.md)
- [Delivery contract](./_shared/delivery-contract.md)
- [Project preferences and supporting UI skills](./_shared/project-preferences.md)
- [Verification policy](./_shared/verification-policy.md)

The [shared preferences](./_shared/project-preferences.md) hold the authoritative default profile. Use the [project preferences template](./_shared/assets/project-preferences.md) for overrides and constraints, inheriting defaults without duplicating them. Do not overwrite existing choices or silently migrate a stack. Respect project-specific conventions and actual user authority. Discover available verification commands and reconcile them with the required verification profile in each target repository.

Supporting upstream UI skills are separate dependencies, not bundled copies. Install selected skills through the host's supported mechanism within user authority, record the source and version/commit, and make them available to the workers that need them. Copying this bundle alone does not install those skills or analysis/browser tools. Carry the verification policy's applicable required tools into the project's design and check contract; omissions or replacements require the human's recorded agreement. Missing dependencies must not appear as applied guidance or passing checks.

## Project outputs

Specs, glossary, design, roadmap, phase plans and delivery checkpoints belong to the project. Their default home is `docs/`, with locations overridden by project instructions. No project documents need to exist before Understand starts.

Keep reusable references in this bundle. Updating or clearing trial outputs must not require deleting skill instructions. Preserve generated work before any user-requested reset; do not interpret installation or a new feature request as permission to reset an existing project.
