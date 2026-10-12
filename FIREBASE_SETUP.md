# Firebase setup for MyHealth Tracker

The public GitHub Pages app currently stores health data in the browser. This repository includes a **draft** Firestore access policy, not an activated cloud backend.

## Intended data model
- Firebase Authentication: Google sign-in and/or email.
- `users/{uid}`: account metadata (avoid medical data here).
- `users/{uid}/profiles/{profileId}`: one independent health profile per person.
- `users/{uid}/profiles/{profileId}/records/{recordId}`: lab and other medical records for that profile.

## Before enabling any uploads
1. Create or select a Firebase project, enable Authentication and Firestore.
2. Register `nedkoradev.github.io` as an authorized authentication domain.
3. Deploy `firestore.rules` in Firebase and test unauthorized access using the Rules Playground or emulator.
4. Implement sign-in, profile switching, per-profile read/write, error handling and explicit one-time migration from localStorage.
5. Test with two different user accounts: neither must be able to read or write the other's data, including by guessing paths.
6. Verify backup/export, account deletion, and recovery. Consider GDPR requirements and data retention before allowing real medical uploads.

**Privacy:** Never commit health records, uploaded PDFs, credentials or private JSON backups to this public repository. The Firebase web configuration is not a secret, but Firestore security rules must be enforced on the server.

**Current status:** No cloud syncing is enabled. Existing local browser records remain untouched.
