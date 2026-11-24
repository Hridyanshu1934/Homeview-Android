# Homeview — Android home dashboard

Homeview is a tablet-first dashboard with a dark, minimal interface. It includes:

- Live clock and date in India time
- Current weather, humidity, feels-like temperature, wind, sunrise and sunset
- Modelled US AQI and PM2.5 from Open-Meteo, with a link to Delhi's official AQI portal
- Spotify and YouTube Music launch links, plus embeddable Spotify/YouTube track, album or playlist URLs
- Google News India headlines (when the feed service is reachable)
- On-device tasks, events and notes saved in local storage
- Echo Dot Bluetooth pairing instructions and a native Android shortcut to Bluetooth settings
- A full-screen Android WebView wrapper that keeps the tablet screen awake

## Important data notes

- The air-quality card is **US AQI from Open-Meteo's model**, not an official CPCB station measurement or India's national AQI scale. Use the in-app CPCB/Delhi live AQI link for official station readings.
- Tasks, events and notes are stored locally on this tablet. They do not sync to Google Calendar or another device in this first version.
- Spotify/YouTube embedded playback is subject to the provider's own sign-in, region, embed and subscription restrictions. Native Echo Dot playback remains controlled by Alexa/Spotify or Bluetooth pairing; this app does not pretend to have full remote control of the Echo.
- Weather, AQI and news require an internet connection.

## Build the APK (recommended: GitHub Actions)

This repository includes `.github/workflows/build-apk.yml`. On a GitHub repository:

1. Upload/push the contents of this folder to a new repository.
2. Open the repository's **Actions** tab.
3. Select **Build Homeview Android APK** and choose **Run workflow** (or let the first push trigger it).
4. When it completes, open the workflow run and download the **Homeview-debug-APK** artifact.
5. Extract the downloaded ZIP. Install `app-debug.apk` on the Android tablet. Android may ask you to allow installation from the browser or file manager you used.

The workflow uses Java 17, Gradle 8.9, Android SDK 35 and produces a debug-signed APK suitable for personal sideloading. It is not a Play Store release build.

## Build locally with Android Studio

1. Install Android Studio with Android SDK Platform 35 and JDK 17.
2. Open this project folder (`Homeview`) in Android Studio.
3. Let Gradle sync; if Android Studio asks for Gradle 8.9, allow it to download/install it.
4. Run **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
5. The debug APK will be under `app/build/outputs/apk/debug/app-debug.apk`.

## App architecture

- `app/src/main/assets/index.html` contains the dashboard UI and client-side logic.
- `app/src/main/assets/manifest.webmanifest` and `sw.js` are included for the optional PWA version when hosted over HTTPS.
- `app/src/main/java/.../MainActivity.java` packages the same UI in Android WebView and exposes the Android Bluetooth Settings shortcut.

## Optional: install as a PWA without an APK

If hosted on an HTTPS static host, open the site in Chrome on Android → browser menu → **Install app** / **Add to Home screen**. The PWA manifest and service worker are already included. The Android APK wrapper is preferable for the integrated full-screen kiosk behavior.
