# Changelog

Storico delle versioni di DartScore, estratto dall'intestazione del sorgente dell'app.

Il file corrente è [`Darts_Score_2_9_2.html`](Darts_Score_2_9_2.html).

---

## v2.9.2

Solo documentazione, nessun cambio funzionale.

- Aggiunta MAPPA DEL FILE e panoramica architetturale nell'intestazione del sorgente, con il flusso stato → render → salvataggio
- 14 intestazioni di sezione nel JavaScript e 8 nel CSS, per orientarsi tra le circa ottanta funzioni senza doverle leggere tutte
- Descrizione di una o due righe sulle funzioni centrali che ne erano prive (`getGara`, `getClassifica`, `buildRow`, `renderHdr`, `updateRow` e altre)
- Riferimenti agli articoli del regolamento raccolti in un unico punto

---

## v2.9.1

Debug del pannello Impostazioni.

- **FIX:** impedita la configurazione con zero incontri — causava `N_SET=0`, `getGara()` restituiva 1-1 su partita vuota e la validazione dichiarava "referto completo" senza alcun incontro giocato
- **FIX:** `setWin` non può superare il numero totale di incontri — prima si poteva impostare una soglia di vittoria matematicamente irraggiungibile
- **FIX:** `maxSub` limitato a 4 (le riserve realmente disponibili) — prima arrivava a 8 pur essendocene solo 4
- **FIX:** limiti ridotti a 24 singoli + 8 doppi (max 32 incontri, erano 60)
- **FIX:** clamp automatico al blur — un valore fuori range viene corretto visivamente invece di essere scartato in silenzio al salvataggio
- **FIX:** pulsante Salva disabilitato con configurazione incoerente, con messaggio esplicativo al posto dell'`alert()` bloccante
- **FIX:** `CFG_LIMITS` spostato prima di `loadCfg()` — era usato prima della dichiarazione nel sorgente (funzionava per ordine di esecuzione)
- `loadCfg()` ripiega sui predefiniti se la combinazione salvata è incoerente

---

## v2.9

- Pannello Impostazioni: numero singoli/doppi, leg per set, best of N, soglia vittoria, max sostituzioni e sistema punti sono configurabili. I valori predefiniti riproducono esattamente il regolamento FIGeST 2026 (verificato: il calendario generato è identico all'originale hardcoded)
- Pulsante "Predefiniti" per ripristinare la configurazione ufficiale
- `CAL` generato da `buildCAL()` con schemi di rotazione `ROT_SINGOLI`/`ROT_DOPPI` invece di array hardcoded — 2 round singoli + 1 round doppi, ciclico
- `legPlayable()` e `toggleLeg()` generalizzati per qualsiasi `MAX_LEG`/`LEG_WIN` (prima assumevano best-of-3 con indici fissi)
- `getPts()` legge il sistema punti da `CFG` invece di valori hardcoded
- `SOMMA_OK` derivata da configurazione; se il sistema punti non produce un totale costante per incontro diventa `null` e la validazione si disattiva
- Modificare le impostazioni azzera la partita in corso, previa conferma

---

## v2.8.1

- Refactoring: estratta `setLabel(fromIdx)` condivisa da `renderSubHistory()` e `renderSubLog()` — elimina ~10 righe di logica duplicata
- **FIX** `populateFrom()`: magic number 20 sostituito con `${N_SET}` nel valore dell'opzione fallback — resta corretto se il calendario cambia
- Rimosso loop ridondante in `saveEdit()`: `refreshUI()` già ricostruisce tutte le righe con i nomi aggiornati
- Meta `color-scheme` sincronizzato in `toggleTheme()`/`applyDark()` — evita flash delle scrollbar in chiaro quando il tema è scuro
- Colonna punti `.rp` allargata da 34px a 36px per i bottoni leg da 40px

---

## v2.8

- **FIX** `toggleLeg`: usa `updateRow(si)` mirato (non `refreshUI`) per non distruggere i bottoni durante il ciclo di tap null→A→B
- **UX:** scroll automatico al prossimo incontro dopo completamento set
- **UX:** bottoni leg aumentati da 33×33 a 40×40px (34px su schermi <360px) per touch target conformi alle linee guida Apple/Google (44pt minimo)
- **UX:** meta description + Open Graph tags per anteprima su WhatsApp/Telegram
- **UX:** `prefers-color-scheme` come default tema — se nessuna preferenza è salvata, rispetta la modalità scura/chiara del sistema operativo
- **Accessibilità:** `@media prefers-reduced-motion` disabilita transizioni
- **PC:** max-width 520px su contenuti principali per leggibilità su desktop
- **Privacy:** aggiunta menzione preferenza tema e Reset completo
- Rimosso toast "Salvato" (feedback non necessario per l'utente)

---

## Versioni precedenti alla v2.8

Le note di rilascio delle versioni dalla 2.0 alla 2.7.1 non sono state trascritte: i file corrispondenti restano consultabili nella [cronologia del repository](https://github.com/Fanza-vibes/DARTSCORE/commits/main).
