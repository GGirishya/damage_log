# IF House Damage Log

A simple shared tool for International Fellowship (IF) to track maintenance and damage reports across its houses (the girls' house, the guys' house, and any others the organization runs).

Anyone with the link — roommates, house managers, or maintenance — can open the page, log something that's broken or needs fixing, and see the same live, shared list update in real time. No login required.

**Live page:** `ggirishya.github.io/damage_log/damage.html`

## What it does

- Log a damage report: which room/house, what happened, how urgent it is, and what the reporter thinks needs to be done.
- Everyone viewing the page sees new reports and status changes instantly (open → in progress → fixed).
- Filter the list by status.
- Update or remove a report as it gets handled.

## How it works

This is a single static web page (`damage.html`) with no server of its own. The shared, real-time list is powered by a free Firebase (Firestore) database — that's what lets multiple people see and update the same list from different devices.

Files in this repo:

- `damage.html` — the page itself (open this to use the tool).
- `firebase-config.js` — connection details for the Firebase project this page talks to. Must stay in the same folder as `damage.html`.

## Using it for another house

Each house could either share this one log (fine for a small org) or get its own copy with its own Firebase project for a fully separate list:

1. Create a free project at [console.firebase.google.com](https://console.firebase.google.com) and enable Firestore Database.
2. In Firestore's Rules tab, allow read/write on a `damages` collection.
3. Register a web app in Project settings and copy the config it gives you into a new `firebase-config.js`.
4. Push `damage.html` and that `firebase-config.js` to a repo, then enable it under Settings → Pages → Deploy from branch.

## A note on the Firebase key

`firebase-config.js` contains a public Firebase API key. This is normal for this kind of app — it identifies the project, it's not a password — and access to the actual data is controlled separately by the Firestore rules, not by hiding this file. Anyone with the key can only do what those rules allow (currently: read and write damage reports, nothing else).