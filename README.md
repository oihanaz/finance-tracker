# Finance Tracker

A private finance tracker that runs in the browser and installs on a phone like an app. This folder holds only the app. It contains no financial data.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app |
| `sw.js` | Lets the app open without internet after the first visit |
| `manifest.webmanifest`, `icon-192.png`, `icon-512.png` | Name and icon for "Install app" |

## 1. Put it on GitHub Pages

1. On github.com, create a new **public** repository, for example `finance-tracker`.
2. Choose **Add file → Upload files**, drag in all the files from this folder, and commit.
3. Open **Settings → Pages**. Under "Build and deployment", pick **Deploy from a branch**, branch `main`, folder `/ (root)`, and save.
4. After a minute or two the app is at `https://YOUR-USERNAME.github.io/finance-tracker/`.

## 2. Install it

- **Phone (Android, Chrome):** open the address, then menu **⋮ → Add to Home screen → Install**. It then opens full screen from its icon.
- **Laptop:** open the same address in Chrome. The install icon in the address bar is optional.

The phone layout (bottom tabs, large balance, compact rows) appears automatically on narrow screens.

## 3. Move your existing data in

In the copy you have been using: Settings (gear icon) → **Save a backup file**. In the hosted app: **Start with my own data**, or tap **Restore a backup** on the first screen. Set a password if you have not already.

## 4. Sync between devices (optional)

The app keeps one encrypted file, `finance-tracker-sync.json`, in your Google Drive. Google never receives anything readable.

**One-time setup in Google Cloud** (menu names may differ slightly):

1. Go to console.cloud.google.com and create a project.
2. **APIs & Services → Library**: search "Google Drive API" and enable it.
3. **OAuth consent screen**: user type External, any app name, your own email. Add your Google account under **Test users**.
4. **Credentials → Create credentials → OAuth client ID**, type **Web application**. Under "Authorized JavaScript origins" add `https://YOUR-USERNAME.github.io` (no path, no trailing slash).
5. Copy the client ID. It ends in `.apps.googleusercontent.com`. It is not a secret.

**In the app**

- First device (the one with your data and a password): Settings → Sync with Google Drive → paste the client ID → **Connect Google Drive**.
- Second device: open the app, go to Settings, paste the same client ID and connect. It asks for your password, then loads your data.

**How it behaves**

- Changes are sent a few seconds after you make them, while you are signed in.
- Google's sign-in lasts about an hour. After that the button at the top reads "Sync · sign in"; one tap renews it. Until then changes stay on the device.
- If both devices changed before syncing, the app asks which copy to keep. The other copy is replaced, not merged.
- Sync needs a password. Unencrypted data is never uploaded.

## Security

| What | Who can see it |
|---|---|
| The app code in this repository | Everyone. It contains no data. |
| Your data on a device | Only someone who can open that device's browser. With a password it is stored encrypted (AES-256). |
| The file in Google Drive | Google stores it but cannot read it. It opens only with your password. |
| Network connections | Only GitHub (to load the app) and, if you turn on sync, Google. The page blocks everything else. |

Things to keep in mind:

- There is no password reset. A forgotten password means the data is gone unless you kept an unencrypted backup.
- The password now also protects the copy in Drive, so use a long one.
- You are trusting GitHub to serve the code you uploaded. Protect the GitHub account with two-factor sign-in.
- Excel exports and bank files you download are not encrypted. Delete them when done.
- Sync is not a history. Keep saving a backup file now and then; it is the only way back to an earlier state.

## Updating the app

Upload the new files over the old ones in the repository. Each device picks up the new version the second time it is opened after that. Your data is not touched by an update, and older backups open in newer versions.
