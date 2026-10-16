# TRIKI Arcade (Android)

Minigry sterowane nasadką Triki. Aplikacja używa Capacitor i Bluetooth LE.

## Automatyczne wydania APK

Push do `main` uruchamia budowanie APK testowego. Wydanie produkcyjne tworzy się
automatycznie po wypchnięciu taga w formacie `vX.Y.Z`, np. `v1.0.3`. Workflow
buduje podpisany APK i dołącza go do GitHub Release jako
`TRIKI-Arcade-X.Y.Z.apk`.

Przed pierwszym wydaniem dodaj w ustawieniach repozytorium GitHub
(`Settings > Secrets and variables > Actions`) następujące sekrety:

- `ANDROID_KEYSTORE_BASE64` — klucz Android zakodowany jako Base64.
- `ANDROID_KEYSTORE_PASSWORD` — hasło do keystore.
- `ANDROID_KEY_ALIAS` — alias klucza.
- `ANDROID_KEY_PASSWORD` — hasło klucza.

Używaj tego samego keystore, którym podpisano poprzednie wersje aplikacji —
zmiana klucza uniemożliwi instalowanie aktualizacji na istniejącej aplikacji.
Tag wydania bez któregokolwiek sekretu zakończy workflow błędem.

Przed wydaniem zaktualizuj wersję w `package.json` i `package-lock.json`
(np. `npm version 1.0.3 --no-git-tag-version`) oraz w `www/index.html`.
Następnie utwórz i wypchnij tag zgodny z tą wersją:

```sh
git tag v1.0.3
git push origin v1.0.3
```