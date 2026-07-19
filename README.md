# NYC · Itinerario 21–30 Agosto 2026 — PWA

Web app mobile-first per seguire l'itinerario di New York: timeline giornaliera con evidenza di attività passate/in corso/prossime (fuso di NYC), spunte salvate sul telefono, mappa interattiva con i pin del giorno e navigazione via Google Maps. Funziona anche offline.

## Contenuto

- `index.html` — l'app completa (dati, UI, logica)
- `manifest.webmanifest` — per installarla sulla home
- `sw.js` — service worker per l'uso offline
- `icon-192.png`, `icon-512.png`, `icon-180.png` — icone app

## Pubblicare su GitHub Pages (5 minuti)

1. Vai su [github.com/new](https://github.com/new) e crea un repository, es. `nyc-itinerario` (pubblico).
2. Nella pagina del repo: **Add file → Upload files** → trascina i 6 file di questa cartella → **Commit changes**.
3. Vai in **Settings → Pages** → sotto "Branch" scegli `main` e cartella `/ (root)` → **Save**.
4. Dopo ~1 minuto l'app è online su `https://TUO-USERNAME.github.io/nyc-itinerario/`

## Installarla sulla home del telefono

**iPhone (Safari):** apri l'URL → tasto Condividi → **Aggiungi alla schermata Home**.
**Android (Chrome):** apri l'URL → menu ⋮ → **Aggiungi a schermata Home** (o banner "Installa app").

Apri l'app una volta con connessione: da quel momento funziona anche offline (le tile della mappa si salvano man mano che le guardi; le zone già viste restano disponibili offline).

## Come funziona

- **Giorno**: selettore orizzontale dei 10 giorni (oggi è evidenziato in rosso). Ogni giornata è divisa in Mattina/Pomeriggio/Sera; la fascia in corso ha il badge "IN CORSO", la prossima attività non spuntata ha il badge "▶ PROSSIMA". Tap su un'attività per spuntarla; 🧭 apre Google Maps con indicazioni in trasporto pubblico.
- **Mappa**: pin numerati nell'ordine di visita, colorati per fascia oraria, con il percorso tratteggiato e il pin dell'hotel. Tap sul pin → naviga.
- **Info**: hotel, voli, biglietti già acquistati, tabella golden hour/tramonto e avanzamento del viaggio.

Le spunte sono salvate in `localStorage` sul telefono (non serve alcun server).

## Modificare l'itinerario

Tutti i dati sono nell'array `DAYS` in cima al `<script>` di `index.html`: nome, coordinate, orario (`time`), nota (`note`), biglietto acquistato (`ticket:true`). Modifica il file e ricarica la pagina su GitHub (il service worker si aggiorna: chiudi e riapri l'app, oppure incrementa `CACHE = "nyc-v2"` in `sw.js` per forzare l'aggiornamento).
