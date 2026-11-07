# IFSE – Application Android

Application Android native (WebView) qui embarque l'application d'inscription IFSE Education :
formulaire, fiche d'inscription en direct, photo d'identité 3,5×4,5 cm, matricule automatique,
et export PDF / impression via le système Android.

- Nom : **IFSE** — package `com.ifse.education` — Android 5.0+ (minSdk 21)
- Fonctionne **hors ligne** (tout est dans `app/src/main/assets/index.html`)

## Obtenir l'APK

### Option A — Android Studio (recommandé)
1. Installer Android Studio, puis **File > Open** et choisir ce dossier.
2. Attendre la synchronisation Gradle.
3. **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
4. L'APK est dans `app/build/outputs/apk/`. Copiez-le sur le téléphone et ouvrez-le
   (autoriser « installer des applications inconnues »).

### Option B — GitHub Actions (sans rien installer)
1. Créer un dépôt GitHub et y envoyer ce dossier.
2. Onglet **Actions > Build IFSE APK** : à la fin, télécharger l'artefact `IFSE-apk`.

### Option C — Ligne de commande
Avec JDK 17 et le SDK Android : `gradle assembleRelease`
(APK : `app/build/outputs/apk/release/app-release.apk`, signé avec la clé debug donc installable).

## Modifier l'application
Éditez `app/src/main/assets/index.html`. Le bouton « Télécharger PDF » appelle le pont
`AndroidBridge.printFiche()` (voir `MainActivity.java`) qui ouvre l'aperçu d'impression Android
(choisir « Enregistrer au format PDF »).

## Publication Play Store
Remplacez `signingConfig signingConfigs.debug` dans `app/build.gradle` par votre propre keystore.
