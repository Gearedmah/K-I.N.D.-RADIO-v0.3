# K.I.N.D. Radio v0.3

Local-first Android music player: one queue, played on the phone or sent to a
Google Cast receiver (TV / stereo) on the same network.

This is the integrated HOME + Genesis source, laid out as a standard Gradle
Android project so it builds as-is.

## Get the APK

Every push runs **Actions > Build KIND Radio APK**. Open the latest run and
download the `KIND-Radio-v0.3-debug-APK` artifact, unzip it, and install
`app-debug.apk` on the phone.

To build locally: `./gradlew :app:assembleDebug` (JDK 17 and the Android SDK
required), or open the folder in Android Studio.

## Layout

- `app/src/main/java/org/kindradio/app/MainActivity.java` — queue and transport; drives local MediaPlayer or Cast
- `app/src/main/java/org/kindradio/app/AudioServer.java` — serves the selected file to the Cast receiver (port 8765, Range support)
- `app/src/main/java/org/kindradio/app/CastProvider.java` — Cast options (default media receiver)
- `app/src/main/assets/kind_radio.html` — the Genesis interface shown in the WebView

## Test sequence

1. Install, open, tap **Add audio files** and pick several songs.
2. Without Cast: play, pause, seek, skip, stop. The queue should match the LCD display.
3. Tap the Cast icon in the top bar, pick the receiver, play a queue item; pause, skip, stop.
4. Disconnect Cast and confirm phone playback resumes control.

## Known limitations

- The audio stream is plain HTTP, reachable by any device on the same network. Use trusted networks only.
- Playback runs only while the app is open (no background service yet).
- Cast state is polled, so connect/disconnect transitions can lag by a moment.
- Debug build only; not a Play Store release.
