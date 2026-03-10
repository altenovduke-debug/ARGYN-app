# CRITICAL BUILD INSTRUCTIONS (SOLVED)

## Android NDK "Clang not found" Error
**PROBLEM:** Flutter build fails with `Android NDK Clang could not be found` even if NDK is installed.

**CAUSE:** Flutter tool fails to detect the NDK path on some macOS environments (M1/M2/M3) especially with newer NDK versions (26+).

**THE WINNING SOLUTION:**
1. Use **NDK 28.2.13676358** (or the latest full version you have).
2. Explicitly set it in `android/app/build.gradle.kts`:
   ```kotlin
   android {
       ndkVersion = "28.2.13676358"
   }
   ```
3. Explicitly set it in `android/local.properties`:
   ```properties
   ndk.dir=/Users/mike/Library/Android/sdk/ndk/28.2.13676358
   ```
4. **IMPORTANT:** Always run the build with the `ANDROID_NDK_HOME` environment variable:
   ```bash
   export ANDROID_NDK_HOME=/Users/mike/Library/Android/sdk/ndk/28.2.13676358
   flutter run
   ```

## Apple Sign-In on Android
To avoid NDK conflicts on Android, the `sign_in_with_apple` logic is wrapped in platform checks. Keep the package in `pubspec.yaml`, but only invoke it on iOS.
