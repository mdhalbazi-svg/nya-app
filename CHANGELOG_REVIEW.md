# Source revision notes

Changes applied to the supplied ZIP:
- Added explicit Android SDK 35 platform/build-tools installation to GitHub Actions.
- Changed the public feed to read from a dedicated `public_reports` collection.
- Restricted full `/reports` documents to their owner and trusted staff in Firestore Rules.
- Added backend publication of a minimised public projection; descriptions, owner IDs, exact coordinates and arbitrary attributes are not copied into the public record. Child report titles are replaced with a generic notice.
- Added basic required-field validation and an email-verification gate before mobile report submission.
- Added a resend-verification-email action.
- Added Urdu privacy and child-safety policy drafts and documented launch blockers.
- Corrected README backend install command to match the workflow's npm install strategy.

Not represented as completed: image upload/EXIF stripping, phone OTP, maps, push notifications, in-app messaging, admin dashboard, user-facing account deletion, complaint UI, full guardian verification, legal review, live Firebase configuration, signing secrets, or a production security audit. These require real project credentials, operational decisions, and end-to-end testing.
