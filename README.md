# Session 2 Android CI/CD

This is a small Android app for demonstrating automated APK builds and releases.
Opening **Session 2 Demo** shows a message from the app built by GitHub Actions.

| Trigger | Build | Where to download |
| --- | --- | --- |
| Push to `main` | Debug APK | Actions → **Build Android APK** → `android-debug-apk` |
| Push a tag such as `v1.0.0` | Signed release APK | Releases → matching version → `app-release.apk` |

The release workflow verifies the APK signature before publishing and also keeps a
copy under the corresponding Actions run. It uses the tag as the Android version
name and the release workflow run number as the version code.

## Release setup

Create a PKCS#12 signing key with alias `session2-release`. In the repository's
Actions secrets, set `ANDROID_KEYSTORE_BASE64` to the base64 encoding of the
keystore and `ANDROID_KEYSTORE_PASSWORD` to its password. Keep the same local
key for future updates. Once main contains the workflow and both secrets exist:

```sh
git tag v1.0.0
git push origin v1.0.0
```

## Local debug build

With JDK 17 and Android SDK 35 installed, run `./gradlew :app:assembleDebug`
or `.\gradlew.bat :app:assembleDebug` on Windows. The result is
`app/build/outputs/apk/debug/app-debug.apk`.
