# RoR2 Stat Calc (Android)

Calcolatore di statistiche per Risk of Rain 2: scegli il sopravvissuto, imposta il livello (1–99),
aggiungi gli item con +/− e le statistiche si aggiornano subito (con indicatore della variazione).
È un fan tool non ufficiale e funziona offline.

## Ottenere l'APK

### Opzione A: GitHub Actions (senza installare nulla)
1. Crea un repository su GitHub e carica il contenuto di questa cartella (compresa `.github/`).
2. Vai in **Actions → Build APK**: la build parte da sola a ogni push (o con "Run workflow").
3. A build finita, scarica l'artefatto **RoR2StatCalc-apk** → contiene `app-release.apk`.
4. Sul telefono abilita "Installa app sconosciute" e installa l'APK.

### Opzione B: Android Studio
1. File → Open → seleziona questa cartella.
2. Se chiede il Gradle wrapper, accetta (Gradle 8.9 o successivo).
3. Build → Build APK(s). L'APK è in `app/build/outputs/apk/`.

### Opzione C: riga di comando (con Android SDK installato)
```
gradle assembleRelease
```

L'APK release è firmato con la chiave di debug: va bene per uso personale, non per il Play Store.

## Modificare dati e formule
Tutto è in `app/src/main/assets/index.html`:
- `CHARS`: statistiche base e per livello dei sopravvissuti
- `ITEMS`: ogni item ha una funzione `apply(s, n)` dove `n` è il numero di copie
- `compute()`: le formule finali (vita, danno, armatura, critico, ecc.)

Note sui calcoli:
- Infusion è considerato già carico al massimo.
- Le statistiche per livello seguono le formule della wiki: vita +30% della base, danno +20%, rigenerazione +20%.
- La rigenerazione da item (Knurl, Slug) scala con il livello.
- I bonus condizionali (Red Whip, Rose Buckler, Cautious Slug) si attivano con la spunta sotto le statistiche.
- Gli effetti che non cambiano una statistica fissa (Crowbar, Focus Crystal, bleed, ecc.) compaiono come elenco "situazionale".
