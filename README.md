# PinRover iOS

iOS build (Capacitor) of the PinRover Base44 app. The web app lives in Base44 and syncs to
`brandonlaraque13/pinrover-social-discovery-for-real-world-places`; this repo only holds the native
shell configuration and the CI that builds it. Each run checks out the latest app source, builds it,
generates the Xcode project and (optionally) uploads to TestFlight.

## Run a build

GitHub → **Actions** → **iOS build** → **Run workflow**.

- `upload` off: compile check for the simulator (no Apple credentials needed).
- `upload` on: signs with the App Store Connect API key and uploads to TestFlight.

## Secrets (Settings → Secrets and variables → Actions)

| Secret | What |
|---|---|
| `SOURCE_REPO_TOKEN` | GitHub token with read access to the Base44 app repo |
| `ASC_KEY_ID` | App Store Connect API key ID |
| `ASC_ISSUER_ID` | App Store Connect issuer ID |
| `ASC_KEY_P8` | Contents of the `.p8` API key file |
| `APPLE_TEAM_ID` | Apple Developer Team ID |

## Native settings

- Bundle ID `com.pinrover.app`, display name PinRover (`capacitor.config.json`).
- Permission texts and the app icon are applied in the workflow (`assets/icon-only.png`, 1024×1024).
- In-app purchase: product `business_monthly`, handled by `@capgo/native-purchases`; the Base44
  `appleIap` function verifies purchases. App Store Server Notifications V2 URL:
  `https://pin-rover.base44.app/functions/appleIap`.
