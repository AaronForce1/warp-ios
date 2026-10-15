# Warp iOS project preferences

**Defaults source:** [Bundled project preferences](../.claude/skills/_shared/project-preferences.md).
**Authority:** The user delegated engineering selection and retains confirmation of product requirements. The latest direction prefers native components and welcomes Expo as distribution middleware.

## User requirements and preferences

- Launch on iPhone and iPad through the App Store; include iCloud app-data sync and iCloud Keychain credential sync in MVP.
- Prefer native UI components. Expo is a distribution-tooling preference to assess, not a mandated runtime.
- Preserve the agreed phone-owned agent/credential and remote-terminal runtime division.
- Direct SSH passwords and keys only for MVP. Bastions, SSH MFA and port forwarding are excluded.

## Engineering direction and alternatives

| Choice | Direction and rationale | Decision/evidence status |
|---|---|---|
| Application runtime | Swift, SwiftUI for app screens, UIKit integration for a terminal view. This aligns with the native-component preference and Apple's lifecycle, CloudKit and Keychain APIs. | Agent-selected design direction under delegated technical authority; no implementation/build yet. |
| Terminal engine | Evaluate SwiftTerm's native iOS/UIKit implementation behind a renderer interface. | Documented candidate; pin a release and validate interactive workloads/performance before commitment. |
| SSH transport | Evaluate a native Swift SSH adapter, initially Citadel/NIOSSH, for password/key authentication, PTY input/output and host verification. | Documented candidate; encrypted keys, resizing, signals and host interoperability require validation. Do not copy insecure sample host-key validators. |
| App data and iCloud | Native local persistence with CloudKit synchronization. Compare Core Data mirroring with an explicit CKSyncEngine adapter against conflict and recovery requirements. | Native APIs documented. Choose one app-data synchronization owner against the agreed data scope and conflict/recovery requirements. |
| Credentials | Protected, synchronizable Keychain storage for SSH credentials and model-provider keys. Host/provider records reference stable credential identifiers. | Explicit user confirmation: iCloud Keychain credential sync is required for MVP; implementation and two-device propagation remain unvalidated. |
| Release pipeline | Evaluate Expo EAS Build/Submit alongside a native Xcode archive/TestFlight pipeline. Prefer the simplest supported pipeline for the chosen native project. | Expo documents native/brownfield EAS support, with feature limitations. A fully Swift project/service configuration remains untested. |
| Alternative app shell | Expo/React Native plus native Swift terminal/SSH/CloudKit modules remains a viable alternative if the release/iteration benefit warrants it. | Not excluded as impossible or non-native. It adds a bridge and language/tooling boundaries to this iOS-only scope; compare actual evidence rather than assuming poorer performance. |

The shared JavaScript package-manager and React/web defaults apply only if a JavaScript/React runtime or tooling package is selected. Expo distribution tooling does not by itself make the app a React Native application. Do not introduce an app manifest or lockfile during architecture planning.

## Supporting skills and verification

The installed Understand, Design and Plan Delivery bundle is used for current records. Implement, Review Change and Orchestrate Delivery apply during an authorized later implementation scope. Expo UI/brownfield and UI UX Pro Max supporting skills are not installed or claimed as applied; assess their applicability when UI/platform work is assigned. Missing visual-design guidance does not prevent the current runtime and synchronization research.

Native application evidence requires actual macOS/Xcode builds and iPhone/iPad simulator or device journeys. This Linux machine does not supply that capability. Follow the [verification policy](../.claude/skills/_shared/verification-policy.md) and keep missing capability visible. App Store publication has not been performed or authorized by merely selecting the distribution target.
