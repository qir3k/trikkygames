# TRIKI Arcade (Android)

Minigry sterowane nasadką Triki. Aplikacja używa Capacitor i Bluetooth LE.

## Build APK

Workflow **Build APK** uruchamia się po pushu. Artefakt pobierzesz z GitHub Actions. Bez klucza podpisu powstaje APK debug, przeznaczone do testów i niezgodne aktualizacyjnie z APK z innych buildów.

## Podpis i aktualizacje

Żeby aktualizować aplikację z jej przycisku **Sprawdź aktualizacje**, skonfiguruj jeden stały klucz podpisu. Wygeneruj go lokalnie tylko raz:

```sh
keytool -genkeypair -v -keystore triki-release.jks -alias triki -keyalg RSA -keysize 2048 -validity 10000
base64 -w0 triki-release.jks
```

W ustawieniach repozytorium GitHub, w **Settings → Secrets and variables → Actions**, dodaj sekrety `ANDROID_KEYSTORE_BASE64` (wynik polecenia base64), `ANDROID_KEYSTORE_PASSWORD`, `ANDROID_KEY_ALIAS` (`triki`) i `ANDROID_KEY_PASSWORD`. Zachowaj plik keystore i hasła w bezpiecznym miejscu. Wszystkie przyszłe wydania muszą być podpisywane tym samym kluczem.

Opublikuj aktualizację tagiem, np. `v1.0.1`. Workflow zbuduje i opublikuje APK jako GitHub Release. W aplikacji wybierz **Sprawdź aktualizacje**, a potem **Pobierz i zainstaluj**; Android poprosi o zgodę i potwierdzenie instalacji. Instalacja bez udziału użytkownika jest blokowana przez Androida.

APK z wcześniejszych buildów debug mogły być podpisane innymi, jednorazowymi kluczami CI. Android nie pozwala zmienić ich podpisu podczas aktualizacji, więc taką starą wersję trzeba odinstalować przed pierwszą instalacją APK podpisanego stałym kluczem. Dane zapisane lokalnie w aplikacji zostaną wtedy usunięte.
