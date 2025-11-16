Eat Orange - One-click GitHub Actions APK builder
------------------------------------------------

How this works (one-click APK from GitHub Actions):
1. Fork this repository to your GitHub account (click 'Fork' in the top-right).
2. Go to your forked repo -> Actions tab.
3. You should see the 'Build Android APK' workflow. Click it.
4. Click 'Run workflow' (or push to main to trigger automatically).
5. Wait a few minutes while GitHub builds the APK.
6. Open the workflow run -> on the right side in 'Artifacts' download 'EatOrange-apk' -> inside you'll find app-debug.apk.
7. Install app-debug.apk on your phone for testing.

Notes:
- The APK is a debug build (works for testing). For Play Store, you'll need to produce a signed release APK.
- If the workflow fails, copy the log link and paste it here; I'll help debug it.

---
Signed Release APK (automated via GitHub Actions)

To create a signed release APK automatically you'll need to:
1. Generate a Java keystore locally:
   keytool -genkeypair -v -keystore release.keystore -alias mykey -keyalg RSA -keysize 2048 -validity 10000

2. Convert the keystore to base64 and add as GitHub secret:
   base64 release.keystore | pbcopy   # macOS (or save output to a file)
   # or
   base64 release.keystore > release.keystore.b64

   In your GitHub repo -> Settings -> Secrets and variables -> Actions -> New repository secret:
   - KEYSTORE_BASE64 : (paste the base64 content)
   - KEYSTORE_PASSWORD : (the keystore password)
   - KEY_PASSWORD : (the key password, often same as keystore password)
   - KEY_ALIAS : (the alias you used, e.g. mykey)

3. After adding secrets, go to Actions -> Build and Sign Android APK -> Run workflow.
   The workflow will produce a signed APK artifact named EatOrange-signed-apk.

If you need help generating the keystore or adding secrets, tell me and I will provide exact commands for your OS.
