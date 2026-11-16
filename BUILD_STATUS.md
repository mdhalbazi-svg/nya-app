# BUILD STATUS (Phase 1: backend foundation)

## IMPLEMENTED BUT NOT EXTERNALLY VERIFIED
- Firestore rules, Storage rules, indexes, firebase.json (not run in Firebase Emulator)
- Cloud Functions: createReport, transitionStatus, runMatching (TypeScript; not compiled here)
- Matching + status-transition logic with vitest tests (written, not executed here)
- GitHub Actions workflow (backend job runs now; Android job auto-skips until android-app/gradlew exists)

## NOT IMPLEMENTED / REQUIRES CONFIGURATION
- Android app, APK/AAB, signing, admin dashboard, web policy pages, FCM alerts, EXIF-stripping function,
  OTP/SMS setup, Maps keys, geographic data import, account deletion, sightings, complaints, rules unit tests
- Firebase project, App Check, first-admin provisioning (set custom claim `role` via Admin SDK script)
