# Changelog

Storico delle versioni di DartScore, estratto dall'intestazione del sorgente dell'app.

Il file dell'app è [`Darts_Score.html`](Darts_Score.html): il nome resta stabile a ogni versione, quella corrente è indicata qui sotto e dentro l'app.

---

## v2.11.0

Accessibilità, conferme interne e una pagina di verifica. **Il calcolo del referto non cambia**: calendario, punteggi, classifica e somma di controllo sono identici, verificati sezione per sezione.

- **I pannelli sono ora veri dialoghi.** I quattro pannelli a scomparsa hanno `role="dialog"`, `aria-modal` e un'etichetta; il focus si sposta dentro all'apertura e torna a chi l'ha aperto alla chiusura; il Tab resta confinato; si chiudono con **Esc**. I modali sono impilati, quindi una conferma aperta sopra le Impostazioni, chiudendosi, restituisce il focus al pannello e non alla pagina
- **Niente più `confirm()` del browser.** Le dieci conferme usano un modale interno, coerente col tema e non bloccante, con etichette specifiche ("Cancella tutto", "Ripristina", "Inizia") al posto del generico OK/Annulla
- **Nuovo [`tests.html`](https://fanza-vibes.github.io/DARTSCORE/tests.html)**: apre l'app e verifica i 20 incontri contro il Referto Gara FIGeST e le regole di punteggio contro il regolamento. Nessuna dipendenza, nessun passaggio di compilazione. Va aperto da un indirizzo web, non con doppio clic: il browser impedisce a una pagina locale di leggerne un'altra
- `window.DS` espone in sola lettura i valori derivati, che essendo dichiarati con `let` non sarebbero leggibili da una pagina di test. Non è usato dall'app

Non si usa il tag `<dialog>` nativo, che richiederebbe Safari 15.4 mentre la compatibilità dichiarata dal progetto parte da Safari 14.

---

## v2.10.0

**Calendario incontri allineato al Referto Gara FIGeST in vigore.** Nessuna modifica al calcolo dei punteggi.

- **I round di singoli erano in ordine sbagliato.** Gli schemi di accoppiamento erano tutti corretti, ma il 2°, 3° e 4° round comparivano in sequenza diversa da quella del referto ufficiale
- **I doppi affrontavano le coppie sbagliate.** L'app faceva incontrare le coppie con la stessa numerazione (C1&C2 contro O1&O2); il referto le incrocia (C1&C2 contro O3&O4, C3&C4 contro O1&O2, e nel secondo round C1&C4 contro O2&O3, C2&C3 contro O1&O4)
- Non era un dettaglio estetico: **ART.5.3** impone di seguire l'ordine indicato sul referto, doppi compresi, e stabilisce che in caso contrario **il leg/set va rigiocato**. Chi seguiva l'app giocava incontri da ripetere
- Tutti e 20 gli incontri generati corrispondono ora al documento ufficiale, verificati uno per uno

Verificato che **nulla al di fuori del calendario sia cambiato**: `getPts`, `getGara`, `getWinner`, `legPlayable`, `norm`, i valori derivati e la somma di controllo (72) risultano identici confrontandoli funzione per funzione prima e dopo la modifica.

Confermato anche dal regolamento 2026, che il resto dell'implementazione già rispettava: 20 set di cui 16 singoli e 4 doppi (ART.2.6), punteggio gara (ART.4.3), massimo 4 sostituzioni con il sostituito che non rientra (ART.5.4), punti individuali validi in singolo e in doppio con lo stesso valore e classifica ordinata per punti, media, set giocati (ART.11.2).

---

## v2.9.5

Cambio di licenza. **Nessuna modifica funzionale: il calcolo del referto è invariato.**

- **Il progetto passa alla [licenza MIT](LICENSE).** Prima era una licenza personalizzata che consentiva solo l'uso "personale, individuale e non commerciale": un circolo o una lega che volesse usarla per il proprio campionato tecnicamente non era autorizzato. Ora uso, modifica, ridistribuzione e vendita sono liberi, a condizione di conservare l'avviso di copyright
- **L'avviso MIT è incluso per intero in testa a `Darts_Score.html`.** L'app viene distribuita anche come file singolo, senza il file `LICENSE` a fianco: senza l'avviso nel file, una copia scaricata non sarebbe conforme alla licenza che la accompagna
- Il piè di pagina dell'informativa privacy non dice più "Tutti i diritti riservati", che contraddiceva la nuova licenza: ora riporta autore e licenza
- README: sezione Licenza riscritta e aggiunta una sezione **Come citare il progetto**, con la riga di credito pronta da copiare. Il credito visibile non è un obbligo MIT, quindi è una richiesta e non una condizione

---

## v2.9.4

Correzione di un errore di calcolo nelle configurazioni personalizzate. **La configurazione FIGeST predefinita non era interessata e non è stata alterata.**

- **FIX: soglia di vittoria raggiungibile da entrambe le squadre.** Il pannello Impostazioni accettava combinazioni in cui il numero di set per la vittoria netta era inferiore o pari a metà degli incontri — per esempio 4 incontri con soglia 2. In quei casi un pareggio perfetto veniva registrato come vittoria netta della squadra di casa, perché `getGara()` valuta `sA` prima di `sB`. Ora `cfgErrors()` richiede una soglia di almeno `⌊totale/2⌋ + 1`, quindi irraggiungibile da entrambe nella stessa partita. Una configurazione incoerente già salvata nel browser viene scartata da `loadCfg()`, che ripiega sui predefiniti
- `norm()`: `\r`, `\n` e `\t` non vengono più cancellati ma trattati da separatori, così `"Mario\nRossi"` diventa `"Mario Rossi"` e non `"Mariorossi"`. Non era raggiungibile dai campi di input, che il browser sanifica da sé: è una correzione di robustezza

Verificato con 112 asserzioni eseguite in un browser sul file reale, e confrontando l'impronta completa del comportamento con i predefiniti FIGeST prima e dopo la modifica: **identica**.

---

## v2.9.3

Accessibilità e distribuzione. Nessuna modifica alla logica di punteggio.

- **Zoom della pagina abilitato**: rimossi `maximum-scale=1.0` e `user-scalable=no` dal viewport. Bloccavano l'ingrandimento (criterio WCAG 1.4.4) e da diverse versioni iOS li ignora comunque, quindi il costo di accessibilità si pagava senza ottenere il comportamento promesso
- `aria-label` sui quattro bottoni di chiusura pannello, gli unici privi di testo visibile. I toggle del tema erano già etichettati
- **Nome file stabile**: l'app è `Darts_Score.html` e non cambia più a ogni versione, così i link condivisi non scadono. I nomi già circolati restano come reindirizzamenti
- **Anteprima di condivisione corretta**: i tag Open Graph stavano solo nel file dell'app, ma il link che si condivide è la radice del sito, che serve `index.html` — dove non c'erano. I crawler non eseguono JavaScript né seguono il meta refresh, quindi l'anteprima ricca introdotta nella 2.8 non poteva funzionare sul link più diffuso. Ora `index.html` porta i tag, immagine inclusa
- `og:description` allineata a ciò che la versione web può davvero garantire: "scaricabile per l'uso offline" invece di "funziona offline"

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
