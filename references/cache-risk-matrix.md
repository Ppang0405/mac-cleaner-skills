# Cache Risk Matrix

Use this matrix to interpret scan output before cleanup.

## Low Risk (usually safe)

- Gradle caches/daemons/wrapper distributions
- CocoaPods cache (`~/Library/Caches/CocoaPods`)
- Xcode `DerivedData`
- npm, yarn, Homebrew download caches
- Project outputs like `node_modules`, `build`, `dist`, `.next`, `.turbo`, `.dart_tool`

Expected impact:
- Larger rebuild or reinstall time after cleanup.

## Medium Risk (safe but verify context)

- Android Studio indexes/caches
- CocoaPods specs repos (`~/.cocoapods/repos`)
- iOS DeviceSupport
- pnpm global store
- Project `Pods` and project `.gradle`

Expected impact:
- Longer next build/install and occasional re-indexing delays.
- Validate toolchain health after cleanup (`pod install`, `npm install`, `gradle build`).

## High Risk (delete only intentionally)

- Android AVD images (`~/.android/avd`)
- CoreSimulator device data (`~/Library/Developer/CoreSimulator/Devices`)
- Xcode Archives (`~/Library/Developer/Xcode/Archives`)

Expected impact:
- Lose emulator/simulator app state or archived build history.
- Keep if you need debugging symbols, app state, or historical release artifacts.

## Safety Rules

- Run scan first and review total reclaimable size.
- Start from low-risk items and rescan.
- Delete high-risk items only with explicit confirmation.
- Never delete custom unknown paths unless intentionally reviewed.
