# Plano de submissão — hoje

---

## PASSO 1 — Hospedar as privacy policies (10 min)

No terminal, a partir desta pasta (github-pages):

```bash
cd "/Users/andremachado/Projetos Pessoais/github-pages"
git init
git add .
git commit -m "Add privacy policies for all apps"
gh repo create axecb6.github.io --public --source=. --push
```

Se o repo axecb6.github.io já existir:
```bash
git remote add origin https://github.com/axecb6/axecb6.github.io.git
git push -u origin main
```

Depois em GitHub → Settings → Pages → Source: main / root → Save.

URLs ficam activas em ~2 min:
- https://axecb6.github.io/manager-foot-drills/privacy/
- https://axecb6.github.io/mindful/privacy/
- https://axecb6.github.io/gringo-game/privacy/
- https://axecb6.github.io/scoreboardsnooker/privacy/

---

## PASSO 2 — Keystores Android (5 min)

### Mindful
```bash
cd "/Users/andremachado/Projetos Pessoais/Mindful"
keytool -genkey -v -keystore mindful.jks \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias mindful \
  -dname "CN=Andre Machado, O=axecb, C=PT"
```
Depois preenche o key.properties (usa key.properties.example como base).

### scoreboardsnooker
```bash
cd "/Users/andremachado/Projetos Pessoais/scoreboardsnooker"
keytool -genkey -v -keystore scoreboardsnooker.jks \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias scoreboardsnooker \
  -dname "CN=Andre Machado, O=axecb, C=PT"
```

### gringo_game
```bash
cd "/Users/andremachado/Projetos Pessoais/gringo_game"
keytool -genkey -v -keystore gringo_game.jks \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias gringo_game \
  -dname "CN=Andre Machado, O=axecb, C=PT"
```

**IMPORTANTE:** Faz backup dos .jks — se os perderes não consegues publicar actualizações.

---

## PASSO 3 — Builds Flutter (10 min cada)

### scoreboardsnooker
```bash
cd "/Users/andremachado/Projetos Pessoais/scoreboardsnooker"
flutter build ipa --release
flutter build appbundle --release
```
IPA → Xcode Organizer → Distribute
AAB → Google Play Console → upload directo

### gringo_game
```bash
cd "/Users/andremachado/Projetos Pessoais/gringo_game"
flutter build ipa --release
flutter build appbundle --release
```

---

## PASSO 4 — Mindful AAB (Android Studio)

Android Studio → Build → Generate Signed App Bundle
→ selecciona mindful.jks → alias mindful → passwords que definiste
→ AAB gerado em app/release/

---

## PASSO 5 — ManagerFootDrills IPA

Xcode → Product → Archive → Distribute → App Store Connect

---

## PASSO 6 — App Store Connect / Play Console (paralelo)

Para cada app criar:
1. Nova app (bundle ID já está correcto)
2. Colar a descrição do STORE_LISTINGS.md
3. Adicionar privacy policy URL
4. Upload screenshots
5. Submit for review

---

## Screenshots rápidas — Simulator

### iOS (iPhone 15 Pro Max — obrigatório)
```bash
# Abre o simulador iPhone 15 Pro Max e faz Command+S para cada ecrã
```

### watchOS (Apple Watch 44mm)
Xcode → Open Simulator → Hardware → Screenshot (⌘S)

### Android (emulador Pixel 8 Pro)
Android Studio → emulador → câmara no lado → Save screenshot
