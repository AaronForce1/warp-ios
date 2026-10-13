# Project preferences and supporting skills

Read this when discovering project preferences, selecting technologies or assigning UI work. Preferences shape the solution; they are not product requirements, installed capabilities or permission to migrate an existing project.

## Resolve and retain preferences

Use the project's declared preferences location, otherwise `docs/PREFERENCES.md`. Reuse an existing equivalent record. When documentation work is authorised and preferences become relevant, use the [preferences template](assets/project-preferences.md) to retain the user's overrides and constraints. Create only a useful record, not a mandatory setup questionnaire. When no overrides are present, state the applicable inherited defaults and proceed within the requested stage. Ask only about material conflicts or missing choices. Preferences already supplied by the user need no repeated confirmation.

Distinguish preferences, must-use constraints, things to avoid and agreed exceptions. Current user direction and explicit project agreement govern. For a new unconstrained project, apply the selected profile's defaults; for an existing project, inspect its design, manifest, package-manager declaration and lockfile. Surface conflicts and obtain agreement before changing an established choice. Never introduce a second lockfile or silently migrate a stack because the bundle has different defaults.

This shared file is the authoritative home for the workflow owner's defaults below. Apply applicable defaults unless current user direction or an agreed project override says otherwise. Record overrides in `docs/PREFERENCES.md` (or the project's declared equivalent), with reason, scope and agreement. An absent project file or omitted preference inherits the shared default; it does not require asking the user to choose again. Existing conflicting project choices must be reconciled before migration. Selected project choices belong in the design; reference this profile and its overrides rather than duplicating the defaults.

## Shared defaults

| Area | Default | Applicability |
|---|---|---|
| Package manager | pnpm | New JavaScript/TypeScript projects; preserve an existing choice until migration is agreed |
| Web components | shadcn/ui with the official shadcn skill | React web; not a native UI requirement |
| UI guidance | frontend-design and ui-ux-pro-max | Relevant visual and interaction work, producing one agreed UI direction |
| React engineering | vercel-composition-patterns and vercel-react-best-practices | Relevant component/performance work; respect framework and version |
| Native UI | Expo building-native-ui | When Expo is selected |
| Testing | Playwright browser journeys for important web outcomes, with focused unit/integration tests | New web test setup; retain suitable existing tests and agree alternatives |

These are overridable preferences. Required verification tools and gate exceptions are governed separately by the [verification policy](verification-policy.md); a preference override cannot silently waive a required check.

Understand reads preferences and asks only about constraints affecting intent or scope. Design resolves relevant choices and exceptions. Plan allocates any needed setup work. Implement and Review follow the agreed project choices and actual configured checks. Missing UI skills must not prevent backend-only work or requirements discovery.

## Supporting UI skills

Keep upstream skills separately installed; do not copy their full instructions into this bundle. Read the installed entrypoint and only relevant supporting references when that work is in scope. A web link is provenance, not evidence that a skill is available or was applied.

| Upstream skill | Responsibility | Applicability |
|---|---|---|
| [Anthropic frontend-design](https://github.com/anthropics/skills/tree/main/skills/frontend-design) | Visual direction, typography, layout and critique | New or materially changed web UI |
| [UI UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | Interaction, accessibility, responsive behaviour and design-system guidance | UI design, implementation and review |
| [Vercel composition patterns](https://github.com/vercel-labs/agent-skills/tree/main/skills/composition-patterns) | Component interfaces, state ownership and composition | React component design and review, proportionate to complexity |
| [Vercel React best practices](https://github.com/vercel-labs/agent-skills/tree/main/skills/react-best-practices) | Rendering, data fetching and performance | React; apply framework/version-specific advice only where compatible |
| [Expo building-native-ui](https://github.com/expo/skills) | Native UI conventions | Expo projects; resolve the named skill in the selected upstream revision |
| [Official shadcn skill](https://github.com/shadcn-ui/ui/tree/main/skills/shadcn) | Existing component selection, composition and styling | React web projects using shadcn/ui |

Record selected skill names, upstream source, installed location and version or commit when available. Disclose unknown revisions. Installation/update follows the user's authority and the host's supported mechanism; a selected skill is not automatically installed by this document. Do not silently substitute a similarly named collection. When unavailable, surface the gap and agree a fallback if it affects the promised outcome; continue unaffected work. Check licenses/notices before vendoring or redistributing upstream content.

The agreed project design governs the UI. Resolve conflicting recommendations explicitly; do not combine competing palettes/layouts or let a supporting skill expand scope or skip our lifecycle handoffs. Use components and semantic tokens to implement one coherent direction. Confirm usability through rendered evidence as described in the [verification policy](verification-policy.md), not through the number of skills invoked.
