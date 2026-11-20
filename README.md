# Level Up: turn it into a real app

This folder holds everything needed to build **Level Up** as an installable phone app.

| File / folder | What it is |
|---|---|
| `www/index.html` | The app itself |
| `assets/logo.png` | App icon |
| `capacitor.config.json` | App name and ID (`Level Up`, `com.levelup.system`) |
| `package.json` | The building blocks the app needs |
| `.github/workflows/android.yml` | Script that builds the Android app in the cloud |

---

## Part 1: Android app (free, no installs, about 15 min)

GitHub builds the app on its own computers, so you don't need to install anything.

### 1. Make a GitHub account
Go to https://github.com and sign up (free).

### 2. Create a repository
1. Click **+** (top right) → **New repository**.
2. Name: `levelup-app`. Choose **Private**.
3. Click **Create repository**.

### 3. Upload the files
1. Unzip `levelup-app.zip` on your PC.
2. On the new repository page, click **uploading an existing file**.
3. Open the unzipped `levelup-app` folder, select **everything inside it** (including the `.github` folder) and drag it into the browser.
4. Click **Commit changes**.

> **Check:** the repository should now show a `.github` folder. If it doesn't, Windows skipped it. Fix it like this:
> click **Add file → Create new file**, type the name `.github/workflows/android.yml`,
> paste the contents of that file from the zip, and click **Commit changes**.

### 4. Let it build
1. Click the **Actions** tab. A run called **Build Android app** starts by itself. If you see a button asking you to enable workflows, click it, then open **Build Android app → Run workflow**.
2. Wait about 5 minutes until it shows a green ✓.
3. Click the finished run, scroll down to **Artifacts** and download **LevelUp-Android**.
4. Unzip it. Inside is **`LevelUp.apk`**, your app.

### 5. Send it to friends (Android)
1. Send `LevelUp.apk` via WhatsApp, Telegram, Google Drive or email.
2. On their phone: tap the file → **Install**.
3. If Android says the source isn't allowed: tap **Settings** → allow **Install unknown apps** for that app (e.g. WhatsApp or Files) → go back → **Install**.
4. If Google Play Protect warns about an "unknown developer", tap **More details → Install anyway**. This shows up for any app that isn't from the Play Store.

### Updating the app later
Change `www/index.html` on GitHub (or upload the new version). Every change rebuilds the app automatically. Download the new APK and send it again. Installing over the old version **keeps everyone's progress**.

---

## Good to know

- **Progress is saved on each phone.** It's private to that person. Uninstalling the app deletes it.
- **Vibration** uses the phone's real vibration motor, and the installed iPhone app can vibrate too (the website version on iPhone can't).
- **Internet** is only needed for the nicer fonts and the Human Benchmark website links. Everything else works offline.

---

## Part 2: Google Play Store (optional, later)

If you want friends to install from the Play Store instead of an APK file:
1. Create a Google Play Console developer account (one-time fee).
2. You'll need a *signed release build* (an `.aab` file) instead of the test APK. Ask Claude to add a release build step to the workflow when you're ready.
3. New personal developer accounts must run a closed test with a group of testers before going public. Your friends can be those testers.

---

## Part 3: iPhone app

Apple only allows iPhone apps to be shared through **TestFlight** or the **App Store**. Both need:
- An **Apple Developer Program** membership (paid yearly), and
- A Mac to build the app. You have Windows, so you'd use a **cloud Mac** service instead, e.g. Codemagic or a GitHub Actions macOS runner.

When you have the Apple Developer account, the steps are:
1. Create the app in App Store Connect with the ID `com.levelup.system`.
2. Connect this GitHub repository to Codemagic (or add an iOS workflow) and add your Apple signing keys.
3. The cloud Mac builds the app and uploads it to TestFlight.
4. Send your friends the TestFlight public link. They install the free **TestFlight** app, tap your link, and get Level Up.

Ask Claude to set up the iOS build step once your Apple account is ready.

---

## Alternative: build on your own PC (Android Studio)

Only if you prefer not to use GitHub:
1. Install **Node.js** (LTS) from https://nodejs.org and **Android Studio** from https://developer.android.com/studio.
2. Open a terminal in the `levelup-app` folder and run:
   ```
   npm install
   npm run android
   ```
3. Android Studio opens. Wait for it to finish loading, then **Build → Build App Bundle(s) / APK(s) → Build APK(s)**.
4. Click **locate** in the pop-up to find `app-debug.apk`.
