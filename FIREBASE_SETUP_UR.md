# Firebase setup — Online Grocery Super Store

The GitHub Pages site currently stores data in the browser only. This guide prepares the secure Firebase connection. Do not enable Firestore test mode for a public shop.

## 1) Create and register the Firebase web app
1. Open https://console.firebase.google.com/ and sign in to the Google account that owns the shop.
2. Create a new project named `online-grocery-super-store` (or select a project you already own).
3. In Project Overview, choose the Web app icon (`</>`), register it as `Online Grocery Store`, and copy the Firebase web config.
4. In Authentication → Sign-in method, enable **Email/Password**.
5. In Authentication → Users, add the shop owner's email/password user. Never put the password in GitHub or send it in chat.
6. In Firestore Database, create the database (production mode is preferred). Choose a nearby supported region carefully; the database location cannot easily be changed later.

Official setup: https://firebase.google.com/docs/web/setup
Authentication: https://firebase.google.com/docs/auth/web/password-auth

## 2) Secure Firestore
1. Open Firestore → Rules.
2. Copy the contents of `firestore.rules` from this repository.
3. In Authentication → Users, open the owner account and copy its **UID**.
4. Replace `REPLACE_WITH_ADMIN_UID` in the rules with that UID, then Publish.

These rules allow customers to submit new orders, but only the owner's authenticated UID can read or manage orders and edit products/settings. Do not publish rules with the placeholder unchanged.

## 3) Send the web config for connection
Share only the Firebase **web app config object** (apiKey, authDomain, projectId, storageBucket if shown, messagingSenderId, appId). These are client configuration values, not service-account private keys. Never share a service-account JSON/private key, passwords, or Google account login.

Once the web config and the admin UID are available, the site code can be connected and tested. Until then, the existing local-only order system remains active.
