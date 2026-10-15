# Native stack, Expo distribution and iCloud feasibility

**Scope:** Documentation/source inspection for the agreed iPhone/iPad, App Store and MVP iCloud requirements. No device build, CloudKit synchronization, signed archive, EAS job or store upload was performed.

## Native UI and terminal candidates

[SwiftTerm's maintained repository](https://github.com/migueldeicaza/SwiftTerm) documents a terminal engine with a UIKit iOS frontend and use in iOS SSH applications. This supports it as a native-terminal candidate, not a performance or complete desktop-compatibility pass. Its current README distinguishes new 2.x APIs from tagged 1.x releases; select and pin an actual release during the feasibility task rather than copying unstable APIs into the application.

[Citadel's maintained repository](https://github.com/orlandos-nl/Citadel) documents password-based SSH, key parsing, PTY/TTY streaming input/output and an underlying NIOSSH implementation. Direct interactive SSH is a credible candidate. Passphrase-protected key formats, resize/control signals, known-host verification and interoperability still require source/build/live checks. Its convenience examples are not production host-trust policy.

## Expo is a runtime and services decision, not an all-or-nothing choice

[Expo Modules API](https://docs.expo.dev/modules/overview/) supports Swift/Kotlin native modules and views. Expo/React Native can therefore include a native terminal and platform adapters. Native-component preference alone is not evidence that Expo cannot satisfy the product.

[Expo's native-app integration documentation](https://docs.expo.dev/brownfield/overview/) defines a native-first app with optional React Native screens as a brownfield scenario. It lists EAS Build and Submit as supported, while describing integration as alpha and warning of feature/documentation gaps. This supports investigating Expo tooling, not claiming a fully Swift project already builds with a particular EAS config.

[EAS Build introduction](https://docs.expo.dev/build/introduction/) describes its standard Expo/React Native build service. [Custom build documentation](https://docs.expo.dev/custom-builds/get-started/) permits custom build steps. [iOS submission documentation](https://docs.expo.dev/submit/ios/) requires a production IPA and Apple developer/app configuration and supports an artifact built with Xcode. Taken together these are leads for native archive/distribution integration; a signed archive and actual service job are the decisive compatibility evidence. No Expo account or Apple credential was used.

**Recommended direction:** native SwiftUI application screens with a UIKit terminal adapter, and independently assess EAS distribution services. Retain Expo/React Native plus native modules as an alternative if supported build/iteration benefits outweigh the added integration boundaries. Do not claim a benchmark-based advantage that has not been measured.

## App-data sync and credential sync are separate mechanisms

[Apple: Mirroring a Core Data store with CloudKit](https://developer.apple.com/documentation/coredata/mirroring-a-core-data-store-with-cloudkit) documents a local replica of the user's CloudKit private database, account requirements and compatible data-model constraints. It does not synchronize a running SSH socket or transfer ownership of an agent coordinator.

[Apple: CKSyncEngine](https://developer.apple.com/documentation/cloudkit/cksyncengine-5sie5) documents app-controlled record synchronization available from iOS/iPadOS 17. Its schedule depends on account/network/power conditions and is indeterminate. Sync state must be persisted. The application remains responsible for account changes, some conflicts and application-specific errors. A private CloudKit database is not an always-immediate distributed runner lock.

[Apple: Synchronizable Keychain items](https://developer.apple.com/documentation/security/ksecattrsynchronizable) describes a separate opt-in synchronization attribute. Passwords, certificates and cryptographic keys can be synchronized on supported OS versions, with restrictions such as incompatibility with device-only accessibility classes and persistent keychain references. General iCloud app-data sync does not enable this automatically. The user subsequently confirmed SSH/model credential synchronization through iCloud Keychain as part of MVP. This establishes product scope, not a tested propagation/result.

## Data and execution boundaries to preserve

- Use an account-specific local replica for the agreed app records; app operation should distinguish local state from pending/succeeded synchronization.
- Reconcile edits and deletion tombstones without duplicating saved hosts or attaching a session to the wrong host.
- Treat synchronized conversations and command records as history. Receiving them must not run commands or silently start an agent on the second device.
- Resolve active-agent ownership at the execution boundary before dispatch. Automatic CloudKit updates cannot enforce single-command ownership or prove a disconnected phone stopped executing.
- Persist stable credential identifiers, not keychain persistent references across devices. No credential values belong in ordinary synchronization records.
- Handle iCloud unavailability/account changes explicitly. The precise no-iCloud user experience remains a product/acceptance detail; do not invent instant sync or silently mix account data.

## Feasibility evidence still needed

Select/pin native candidates and perform a real Xcode terminal/SSH build, validate the persistence helper on representative prepared hosts, exercise two iCloud-linked devices under updates/offline/account-change scenarios, and validate a signed native archive with the selected release service. App Store review is a later external outcome, not established by documentation.
