# Warp-account integration feasibility — initial disposition

**Method:** read-only official-documentation and maintained desktop-source inspection. No Warp account login, credential extraction, API operation, agent run, mobile build or entitlement test was performed.
**Requirement:** [INTEGRATION-01](../specs/product-foundation.md#integration-01-assess-warp-account-feasibility).
**Disposition:** a documented external integration path exists for Warp cloud/factory agent run control. Reusing a Warp account for this MVP's phone-owned model inference remains unresolved; it is not established by the cloud-run API.

## Documented supported path

[Warp Platform API](https://docs.warp.dev/api/) documents creating/managing/querying factories and cloud agent runs, authenticated with a Warp API key from account settings. [Agent/run API and SDK documentation](https://docs.warp.dev/factories/api-and-sdk/) describes raw REST access and Python/TypeScript SDKs. This is evidence of an external API contract rather than merely an internal function named public API.

[API-key documentation](https://docs.warp.dev/agents/cli/oz-cli/api-keys/) distinguishes personal, agent and self-hosted-worker authentication/ownership. Account/team access and billing must be assessed for a selected integration scope; documentation does not prove this user has enabled access or any particular allowance.

[Cloud harness authentication documentation](https://docs.warp.dev/platform/harnesses/authentication/) describes credentials for cloud agent harnesses. It does not establish that the same service exposes a general account-backed model-inference endpoint for a phone-owned coordinator.

## What could be added later

A native iOS API adapter could present/run-status management against the documented REST contract, subject to authorized account access and actual mobile compatibility testing. This is a credible research direction for later cloud agent management. It does not require making a hosted agent the MVP default.

The documented authentication path is user-provided API-key access. A polished mobile account sign-in/OAuth flow, provider access billed to a Warp account, and entitlement to the required model features are distinct questions. No universal impossibility claim is made; they need an explicitly supported contract before being promised.

## Desktop-source evidence and reuse boundary

The selected desktop source contains authenticated request helpers in `crates/warp_server_client/src/public_api.rs`, account/token management in `auth/session.rs` and `base_client.rs`, and provider configuration in `crates/ai`. These clarify current first-party implementation, not an independently supported consumer mobile-login contract. Some remote paths spawn SSH processes; direct reuse on iOS cannot be assumed.

The desktop repository is principally AGPL-licensed, with designated UI-framework components under MIT. Any actual reuse must identify the relevant files/dependencies and obligations; using a documented HTTP interface is a different design choice from copying app crates. No source was copied into the iOS application and no legal/redistribution conclusion is claimed.

## Remaining evidence needed for a named integration

- Select whether the desired feature is cloud-run management, mobile login, account-backed inference, or some combination; preserve the phone-owned BYOK MVP.
- Confirm official authentication/endpoint/account scopes for that feature and document product data/credential flow.
- With authorized access, exercise the scoped native HTTP/sign-in/entitlement flow and record failures/account prerequisites. API documentation alone is not a live result.
- If source reuse is selected, assess native compilation/portability and the actual file/dependency license obligations.

## Effect on MVP

Continue the four-provider BYOK path independently. The initial feasibility investigation found an actionable documented cloud-run integration path and isolated the unresolved phone-inference/mobile-login premise. There is no missing Warp token blocking current local requirements/design/planning work.
