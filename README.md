# MyReminders — Android Reminder App

A simple Android app (built with Capacitor, so no Android Studio needed) that reminds you
about anything: work tasks, medication, your brand, meetings, report deadlines, etc.

## Features
- Custom categories with emojis (Work 💼, Tasks ✅, Medication 💊, Brand 🏷️, Meetings 🤝, Reports 📊, + your own)
- Add a title + notes to every reminder
- Repeat options: One time / Daily / Weekly / Monthly / Quarterly
- Real Android notification popup + sound + vibration when it's due
- Snooze (10 min) or Dismiss actions right on the notification
- Everything stored locally on your phone (no account, no server, no internet needed to run it)

## How to get the installable APK using only a GitHub account (no Android Studio, no laptop setup)

1. Create a new **empty** repository on GitHub, e.g. `myreminders`.
2. Upload all the files in this folder to that repository (keep the same folder structure —
   `www/index.html`, `capacitor.config.json`, `package.json`, and the `.github/workflows/build-apk.yml` file).
   Easiest way on the GitHub website: "Add file" → "Upload files", drag the whole folder contents in, and commit.
3. Go to the **Actions** tab of your repository. A workflow called **"Build Android APK"** will run automatically
   (it also runs any time you push a change). Wait for it to finish (a few minutes, green checkmark).
4. Open that finished workflow run → scroll to **Artifacts** → download **MyReminders-debug-apk** (a .zip).
5. Unzip it on your phone (or unzip on your PC and transfer `app-debug.apk` to your phone).
6. On your Android phone, tap the `.apk` file to install it. Android will warn about "unknown sources" —
   allow installation from that source (this is normal for apps installed outside the Play Store).
7. Open the app, allow the notification permission when asked, and start adding reminders.

## Updating the app later
Just edit `www/index.html` (or any file) in the GitHub repo and commit — GitHub Actions will rebuild
a fresh APK automatically every time. Download the new one from the Actions tab the same way.

## Adding your own custom ringtone (instead of the default notification sound)

Just **one push** needed — no waiting on a generated commit, no typing paths in the GitHub upload box.

1. Your sound file is already placed at `sound/alarm_tone.mp3`, and `capacitor.config.json` /
   `www/index.html` are already set to use that exact file — no extra editing needed.
   (If you ever swap in a different file, keep the name `alarm_tone` and update the `sound`
   value in `capacitor.config.json` and the `CUSTOM_SOUND` value in `www/index.html` to match
   its extension.)
2. Push/commit everything to your repo as normal (see the steps above).
3. The workflow will automatically copy your file into the Android project and build a fresh APK
   with your custom sound.
4. **Uninstall the old app from your phone before installing the new APK** — Android locks a
   notification channel's sound the first time it's created, so a fresh install (new channel ID)
   is the reliable way to make sure the new tone takes effect.

## Notes on reliability
- For best results, once installed, open Android's battery settings for the app and disable
  "battery optimization" for it, so the system doesn't stop it from firing reminders in the background.
- The app itself never needs internet after installation — it works fully offline.
