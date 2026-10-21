# TinkerHub Sticker Book

Every sticker TinkerHub has designed, stuck on one 3D laptop. Click a sticker to read what it means and who designed it, rate it, and count your collection on the live leaderboard.

The whole site is one file: `index.html`. Sticker images and the Drowner font are embedded in it.

## 1. Put it on GitHub

1. Create a new repository on github.com (for example `tinkerhub-sticker-book`).
2. Upload `index.html`, `.nojekyll`, `firestore.rules` and this `README.md`, or push them from your computer:
   ```bash
   git init
   git add .
   git commit -m "TinkerHub Sticker Book"
   git branch -M main
   git remote add origin https://github.com/<your-username>/tinkerhub-sticker-book.git
   git push -u origin main
   ```

## 2. Host it with GitHub Pages (free)

1. In the repository, open **Settings → Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`, and save.
3. After a minute the site is live at `https://<your-username>.github.io/tinkerhub-sticker-book/`.

Every time you commit a change to `main` (from your computer or by editing the file on github.com), GitHub Pages republishes the site automatically, usually within a minute or two.

A custom domain (for example `stickers.tinkerhub.org`) can be added in the same Pages settings.

## 3. Turn on the public leaderboard and ratings (Firebase, free tier)

Anyone who visits gets a private anonymous ID, so they can add their name, count their stickers and rate, without signing up.

1. Go to <https://console.firebase.google.com>, create a project, and add a **Web app** (the `</>` icon). Copy the `firebaseConfig` object it shows you.
2. **Build → Authentication → Get started → Sign-in method**: enable **Anonymous**.
3. **Authentication → Settings → Authorized domains**: add `<your-username>.github.io` (and your custom domain if you use one).
4. **Build → Firestore Database → Create database** (production mode).
5. **Firestore → Rules**: replace everything with the contents of `firestore.rules` and click **Publish**.
6. Open `index.html`, find the line

   ```js
   window.FIREBASE_CONFIG = window.FIREBASE_CONFIG || null;
   ```

   and replace `null` with your config, for example:

   ```js
   window.FIREBASE_CONFIG = window.FIREBASE_CONFIG || {
     apiKey: "…",
     authDomain: "….firebaseapp.com",
     projectId: "…",
     storageBucket: "….appspot.com",
     messagingSenderId: "…",
     appId: "…"
   };
   ```

   (The Firebase web config is meant to be public; the rules in `firestore.rules` are what protect the data.)
7. Commit and push. The "Live" dot in the Leaderboard turns red when it's connected.

Note: the copy of the site on claude.ai keeps its own leaderboard. Entries made there don't move to Firebase.

## Editing content

- **Sticker text, designers, portfolio links:** search `index.html` for `const STICKERS =`. Each sticker has `title`, `meaning`, `inspo`, `designer` and `portfolio`.
- **Firebase settings:** the `FIREBASE_CONFIG` block near the top of the scripts.

## Adding more sections later

Keep `index.html` as the home page and add new pages next to it (for example `about.html`, `events/index.html`). GitHub Pages serves them at `/about.html` and `/events/`. Link to them from the Menu by adding a button inside `<div class="menu">`.
