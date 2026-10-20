# Kxko Diagrams Admin App — patch

This patch changes the Android app's home screen into a WebView shell for the existing admin dashboard while preserving Firebase Cloud Messaging topic subscription, device registration, and Android 13+ notification permission handling.

## Files
- `app/src/main/java/com/kxko/dailybriefing/MainActivity.kt` — replacement activity.
- `app/src/main/AndroidManifest.xml` — cleaned manifest (the original listed the FCM service twice).

## Apply
Copy both files into the same paths in the `Kxko-brief` Android project, replacing the existing files. No new Gradle dependencies are required.

## Important checks before installing
1. Confirm the published admin page is actually available at `https://kxko4b.github.io/diagrams/admin/`. If GitHub Pages is configured with a different custom domain or base path, change `ADMIN_URL` and `ADMIN_HOST` in `MainActivity.kt` accordingly.
2. Build and run from Android Studio, then test sign-in, navigation, review/question/request editing, and image/file upload.
3. The app uses the existing website's Supabase client and authentication. It does **not** embed a Supabase service-role key or any new secrets.
4. Existing push notification delivery still depends on the Firebase project configuration and the current `MyFirebaseMessagingService` implementation.

## Scope
This is a first working shell around the existing web admin, not a full native rewrite. It is the quickest way to reuse the current dashboard functionality on a phone without duplicating its Supabase data logic. External links open in the browser; the dashboard itself stays in the app.
