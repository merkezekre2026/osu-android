# Building osu! for Android via GitHub Actions

This repository is pre-configured to automatically compile the official **osu!lazer** Android application using GitHub Actions.

## How to Build

1. **Push this repository to your GitHub account:**
   - Create a new repository on GitHub (e.g. `yourusername/osu-android`).
   - Run the following commands in this directory to upload your code to GitHub:
     ```bash
     git remote add origin https://github.com/yourusername/osu-android.git
     git branch -M main
     git push -u origin main
     ```

2. **Trigger the GitHub Action:**
   - Go to the **Actions** tab of your repository on GitHub.
   - Select the **Build osu! Android APK** workflow in the left sidebar.
   - Click the **Run workflow** button to start the build manually (alternatively, the build will trigger automatically every time you push to the `main`/`master` branch).

3. **Download the APK:**
   - Once the build workflow completes successfully (takes around 10-15 minutes), click on the completed run.
   - Scroll down to the **Artifacts** section at the bottom of the page.
   - Download the `osu-android-apk` zip file.
   - Extract it and install the `.apk` file on your Android device!

## APK Signing (Optional)

By default, the workflow produces an unsigned or debug-signed Release APK. If you want to configure secure signing for publishing or update compatibility:
1. Generate an Android Keystore file.
2. Add your Keystore file and credentials to GitHub Repo Secrets (Settings -> Secrets and variables -> Actions).
3. Update the build step in `.github/workflows/build-android.yml` with the following parameters:
   ```bash
   dotnet publish osu.Android/osu.Android.csproj -c Release -f net8.0-android -p:AndroidKeyStore=true -p:AndroidSigningKeyStore=keystore.jks -p:AndroidSigningStorePass=${{ secrets.KEYSTORE_PASSWORD }} -p:AndroidSigningKeyAlias=${{ secrets.KEY_ALIAS }} -p:AndroidSigningKeyPass=${{ secrets.KEY_PASSWORD }} -o ./build-output
   ```
