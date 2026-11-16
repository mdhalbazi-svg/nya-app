# Lost & Found Pakistan — Android source foundation

Package: `pk.lostfound.pakistan`  
Minimum Android: API 24 | Target: API 35 | JDK 17 | Gradle 8.9

## Included
- Native Android app source (Kotlin)
- Email/password Firebase Authentication
- Public approved-report feed
- Report submission through the existing callable Cloud Function
- Email-verification gate before report submission
- Public report feed reads a minimised `public_reports` projection, not private report records
- Backend-only publication projection; private descriptions, owner IDs and precise coordinates are not exposed by the public feed
- Firebase backend rules, indexes and Cloud Functions from the supplied source
- GitHub Actions workflow for backend tests and Android APK/AAB build

## Required before a real deployment
This ZIP is source code, not a signed release. A real Firebase project and owner-controlled credentials are required. Do not publish with placeholder configuration.

1. Create a Firebase project and register Android app ID `pk.lostfound.pakistan`.
2. In Firebase Console enable Email/Password Authentication, Firestore, Storage, Functions and App Check.
3. Add these Gradle properties to `~/.gradle/gradle.properties` or GitHub Actions Gradle properties:
   - `FIREBASE_API_KEY`
   - `FIREBASE_APP_ID`
   - `FIREBASE_PROJECT_ID`
   - `FIREBASE_SENDER_ID`
4. Deploy backend from `backend/` using Firebase CLI after reviewing the rules and setting the correct project.
5. Configure App Check for Android (Play Integrity). For debug builds, retrieve the Firebase App Check debug token from Logcat and register it in Firebase Console. Enforce App Check only after valid clients are registered.
6. Set GitHub Actions secrets `KEYSTORE_BASE64`, `KEYSTORE_PASSWORD`, `KEY_ALIAS`, `KEY_PASSWORD` for signed release output. Never commit a keystore.
7. Complete the Play Console Data safety form, publish the policy templates in `policies/` at public HTTPS URLs after legal review, and implement account deletion and child-safety/moderation processes. The included templates are drafts, not legal advice or publication-ready policy pages.

## Important functional limitations and launch blockers
This is an improved source foundation, **not a finished or independently audited production app**. The current mobile UI supports email/password accounts, email verification before report submission, report submission and browsing minimised approved public reports. The public feed now reads from `public_reports`; previously deployed data must be migrated/re-published through a trusted admin process before it appears. App Check uses the debug provider in debug builds and Play Integrity in release builds.

Not implemented: photo upload and EXIF sanitisation pipeline, phone OTP, maps/location picker, push alerts, in-app messaging, admin/moderator dashboard, user-facing account deletion, complaint/report-abuse interface, full guardian identity verification, and end-to-end moderation tooling. The backend's publication projection intentionally omits descriptions, owner IDs, exact coordinates and child details from the public feed. A moderator must still review and publish reports through a trusted administrative process; that admin interface is not included.

**Do not publish or advertise this build as a fully operational missing-child response service.** Before public launch, implement and test all missing functions, publish a real privacy policy and child-safety standards at public HTTPS URLs, provide account/data deletion, establish a staffed moderation and law-enforcement escalation process, conduct Firebase Rules/App Check tests, and complete Google Play Data safety and target-audience declarations. Contact police immediately for missing children or immediate danger; the app is not an emergency service.

## GitHub upload layout
Extract the ZIP and upload the complete `lost-found-pakistan` folder to the GitHub repository, preserving the outer folder. The workflow paths are written for that layout.

## Build locally
Install Android Studio / Android SDK 35 and JDK 17. From this directory:
`gradle :app:assembleDebug`
`gradle :app:bundleRelease`

## Backend
From `backend/`:
`npm install --prefix functions`
`npm --prefix functions run build`
`npm --prefix functions test`
`firebase deploy --only firestore,storage,functions`
