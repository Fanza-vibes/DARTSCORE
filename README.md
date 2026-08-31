# DARTS SCORE

App web per il calcolo dei punteggi nelle partite di freccette.

## ▶ Apri l'app online

👉 **[Avvia DartScore](https://fanza-vibes.github.io/DARTSCORE/)**

Nessuna installazione necessaria. Si apre direttamente nel browser.

---

## Descrizione

Darts Score è un'applicazione single-page pensata per calcolare in modo rapido e preciso i punteggi di una partita di freccette, gestendo automaticamente set, leg, squadre e giocatori secondo il regolamento ufficiale FIGeST 2026.

### Funzionalità principali

- Gestione completa di **squadre e giocatori** con modifica nomi anche durante la partita
- Calcolo automatico di **set e leg** secondo il regolamento ufficiale (ART.4.3)
- **Sostituzioni** con cronologia, annullamento e validazione (max 4 per squadra, ART.5.4)
- **Classifica individuale** con punti, media e set vinti (ART.11.2)
- Riepilogo dettagliato con **validazione somma punti** (ART.15.1)
- **Esportazione PDF** del referto gara tramite stampa nativa (zero dipendenze)
- **Impostazioni gara configurabili**: numero di incontri singoli e doppi, leg per set,
  best of N, soglia di vittoria, sostituzioni massime e sistema punti
- **Tema chiaro e scuro** con switch rapido e rispetto della preferenza di sistema
- Interfaccia mobile-first, ottimizzata per l'uso a bordo campo
- **Funziona offline** con il file scaricato in locale; sulla versione web dipende
  dalla cache del browser e non è garantito
- Nessun account, nessuna registrazione, nessun dato inviato a server

### Novità v2.9.2

- **Pannello Impostazioni Gara**: incontri singoli e doppi, leg per vincere il set,
  leg massimi (best of N), set per la vittoria netta, sostituzioni massime e
  sistema punti sono ora tutti configurabili
- I valori predefiniti riproducono esattamente il **regolamento FIGeST 2026**;
  il pulsante **"Predefiniti"** ripristina la configurazione ufficiale
- Calendario incontri **generato dinamicamente** dalla configurazione, con schemi
  di rotazione per singoli e doppi al posto degli elenchi fissi
- Calcolo di leg, set e punti generalizzato: funziona con qualsiasi formato,
  non solo il best-of-3 del regolamento
- Validazione della configurazione: combinazioni incoerenti (zero incontri,
  soglia di vittoria irraggiungibile) vengono bloccate con messaggio esplicativo
  e i valori fuori range corretti automaticamente
- La modifica delle impostazioni azzera la partita in corso, previa conferma
- Le impostazioni vengono salvate nel browser e ripristinate alla visita successiva
- Sorgente documentato: mappa del file, intestazioni di sezione e descrizione
  delle funzioni principali

<details>
<summary>Versioni precedenti</summary>

**v2.9.1** — correzioni al pannello Impostazioni: limiti coerenti sui campi,
clamp automatico dei valori fuori range, salvataggio disabilitato con
configurazione incoerente.

**v2.8.1** — refactoring interno, sincronizzazione del meta `color-scheme`
al cambio tema, colonna punti allargata per i bottoni leg.

**v2.8** — tema scuro con toggle in ogni schermata, bottoni leg ingranditi,
scroll automatico al prossimo incontro, modifica nomi squadre durante la partita,
reset completo dei dati salvati, banner stato partita, supporto animazioni
ridotte, anteprima link su WhatsApp/Telegram.

Storico completo e dettagliato in [CHANGELOG.md](CHANGELOG.md).

</details>

---

## Come usarla

### Versione web (consigliata)

Il modo più semplice è aprire direttamente il link:

👉 **[https://fanza-vibes.github.io/DARTSCORE/](https://fanza-vibes.github.io/DARTSCORE/)**

Funziona su qualsiasi browser moderno, da telefono o da computer.

> **Uso offline:** la versione web richiede la connessione per l'apertura. Il browser
> può conservare la pagina in cache e riaprirla senza rete, ma è un comportamento
> non garantito e la cache può essere svuotata in qualsiasi momento. Se ti serve la
> certezza di poter aprire l'app a bordo campo senza connessione, scarica il file
> (vedi [Versione scaricabile](#versione-scaricabile-uso-offline-completo)).

**Per aggiungerla alla schermata home del telefono (opzionale):**

- **iPhone (Safari):** tocca l'icona di condivisione ↑ → "Aggiungi a schermata Home"
- **Android (Chrome):** tocca i tre puntini ⋯ → "Aggiungi a schermata Home"

In questo modo si comporta come un'app vera, senza barra del browser.

---

### Versione scaricabile (uso offline completo)

Se preferisci avere il file in locale senza dipendere da internet:

#### Da telefono (iPhone o Android)

1. Apri questo link nel browser del telefono: [github.com/Fanza-vibes/DARTSCORE](https://github.com/Fanza-vibes/DARTSCORE)
2. Nella lista dei file, tocca il nome **`Darts_Score_2_9_2.html`**
3. Si aprirà una pagina con il contenuto del file. In alto a destra tocca l'icona **"⋯"** (tre puntini) oppure il pulsante **"Raw"**
4. Se hai toccato **"Raw"**: si aprirà una pagina con solo testo. Tocca l'icona di condivisione del browser (su iPhone il quadrato con la freccia verso l'alto ↑, su Android i tre puntini del browser) e scegli **"Scarica"** oppure **"Salva pagina"**
5. Se hai toccato **"⋯"** (tre puntini): scegli **"Download"** dal menu che appare

> **Alternativa più semplice da telefono:** dalla [pagina principale del progetto](https://github.com/Fanza-vibes/DARTSCORE), scorri in basso e tocca il pulsante verde **"<> Code"**, poi **"Download ZIP"**. Apri lo ZIP scaricato e troverai il file `.html` all'interno.

#### Da computer

1. Vai alla pagina del progetto: [github.com/Fanza-vibes/DARTSCORE](https://github.com/Fanza-vibes/DARTSCORE)
2. Clicca sul file **`Darts_Score_2_9_2.html`** nella lista
3. Clicca il pulsante **"⬇ Download raw file"** (icona con freccia verso il basso, in alto a destra)
4. Il file verrà salvato nella cartella *Download* del tuo computer

In alternativa, dalla pagina principale clicca il pulsante verde **"<> Code"** → **"Download ZIP"** per scaricare l'intero progetto.

> **Nota:** non serve installare nulla. Il file `.html` si apre direttamente con qualsiasi browser con un doppio clic.

---

## Compatibilità

| Browser | Versione minima |
|---------|----------------|
| Chrome  | 88+            |
| Firefox | 78+            |
| Safari  | 14+            |
| Edge    | 88+            |
| Opera   | 74+            |

Testato con fix cross-browser per `dvh`, `inset`, `env()`, `appearance` e `color-scheme`.

Ottimizzazioni specifiche per iOS Safari: gestione touch event, `pagehide` per salvataggio, `visibility:hidden` sui pannelli, safe-area-inset.

---

## Privacy e dati

I dati inseriti nell'app (nomi squadre, nomi giocatori, risultati) vengono gestiti **esclusivamente in locale** nel browser tramite `localStorage` e non vengono mai trasmessi allo sviluppatore. I dati vengono eliminati automaticamente dopo 48 ore oppure all'avvio di una nuova partita. La preferenza del tema (chiaro/scuro) e le impostazioni di gara (numero incontri, sistema punti) vengono salvate separatamente e non contengono dati personali.

La versione web è ospitata tramite **GitHub Pages** (Microsoft/GitHub). Ogni accesso alla pagina genera automaticamente sui server di GitHub un log tecnico standard (indirizzo IP, browser, timestamp). Questi dati sono trattati da GitHub come responsabile del trattamento ai sensi del GDPR — lo sviluppatore non vi ha accesso. Per dettagli, consulta la [GitHub Privacy Statement](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement).

Per l'informativa completa consulta la sezione **🔒 Informativa Privacy** all'interno dell'app.

---

## Sicurezza

L'app implementa una Content Security Policy (CSP) che blocca il caricamento di risorse esterne (script, font, immagini da CDN). Tutti gli input utente vengono sanitizzati tramite escape HTML per prevenire XSS. Non vengono utilizzate dipendenze esterne di alcun tipo.

---

## Licenza

**Solo uso personale e non commerciale.**

Vedi il file [LICENSE](LICENSE) per i termini completi.

Per richieste di licenza commerciale, contattare tramite questo repository.
https://github.com/Fanza-vibes/DARTSCORE

Email:
jackal.trail2027@eagereverest.com
