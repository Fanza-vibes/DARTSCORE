# DartScore

Referto gara digitale e segnapunti per freccette **Soft Dart**, conforme al regolamento **FIGeST 2026**. Gratis, senza installazione: si usa dal browser o si scarica per giocare offline.

## ▶ Apri l'app online

👉 **[Avvia DartScore](https://fanza-vibes.github.io/DARTSCORE/)**

Nessuna installazione necessaria. Si apre direttamente nel browser.

## Schermate

| Setup squadre | Referto in corso | Riepilogo (tema scuro) |
|:---:|:---:|:---:|
| <img src="docs/screenshot-setup.png" width="230" alt="Schermata di inserimento squadre, categoria e giocatori"> | <img src="docs/screenshot-referto.png" width="230" alt="Referto con assegnazione dei leg incontro per incontro"> | <img src="docs/screenshot-riepilogo.png" width="230" alt="Riepilogo con punteggio gara, classifica individuale e dettaglio incontri"> |

---

## Descrizione

DartScore è un'applicazione single-page pensata per calcolare in modo rapido e preciso i punteggi di una partita di freccette, gestendo automaticamente set, leg, squadre e giocatori secondo il regolamento ufficiale FIGeST 2026.

### Funzionalità principali

- Gestione completa di **squadre e giocatori** con modifica nomi anche durante la partita
- Calcolo automatico di **set e leg** secondo il regolamento ufficiale (ART.4.3)
- **Sostituzioni** con cronologia, annullamento e validazione (max 4 per squadra, ART.5.4)
- **Classifica individuale** con punti, media e set vinti (ART.11.2)
- Riepilogo dettagliato con **validazione somma punti** (ART.15.1)
- **Esportazione PDF** del referto gara tramite stampa nativa (zero dipendenze)
- **Impostazioni gara configurabili**: numero di incontri singoli e doppi, leg per set,
  best of N, soglia di vittoria, sostituzioni massime e sistema punti
- **Guida all'uso integrata**, con le regole predefinite FIGeST spiegate passo per passo
- **Tema chiaro e scuro** con switch rapido e rispetto della preferenza di sistema
- Interfaccia mobile-first, ottimizzata per l'uso a bordo campo
- **Funziona offline** con il file scaricato in locale; sulla versione web dipende
  dalla cache del browser e non è garantito
- Nessun account, nessuna registrazione, nessun dato inviato a server

### Novità

**v2.12.0** — Nuovo tasto **ⓘ Guida** nella schermata iniziale: spiega in otto punti come si usa l'app, dai leg ai punti, dai cambi al riepilogo.

**v2.11.0** — I pannelli si chiudono con **Esc** e sono navigabili da tastiera e screen reader; le conferme non usano più le finestre del browser. Aggiunta una [pagina di verifica](https://fanza-vibes.github.io/DARTSCORE/tests.html) che controlla il calendario contro il Referto Gara ufficiale.

**v2.10.0** — **Calendario incontri allineato al Referto Gara FIGeST in vigore**: i round di singoli erano in ordine diverso da quello ufficiale e nei doppi le coppie si affrontavano con la stessa numerazione invece di incrociarsi. Il regolamento (ART.5.3) impone di seguire l'ordine del referto, pena la ripetizione del set.

**v2.9.5** — Il progetto passa alla **licenza MIT**: uso, modifica, ridistribuzione e vendita liberi, a condizione di conservare l'avviso di copyright. Vedi [Licenza](#licenza).

**v2.9.4** — Corretta una configurazione personalizzata che poteva registrare un pareggio come vittoria netta. I valori predefiniti FIGeST non erano interessati.

**v2.9.3** — Zoom della pagina abilitato, etichette per screen reader, nome file stabile che non fa scadere i link condivisi, anteprima di condivisione corretta.

**v2.9** — **Pannello Impostazioni Gara**: numero di incontri, leg per set, best of N, soglia di vittoria, sostituzioni e sistema punti diventano configurabili, con i predefiniti che riproducono il regolamento FIGeST 2026.

📖 Storico completo di tutte le versioni: **[CHANGELOG.md](CHANGELOG.md)**

🔧 Procedura di rilascio e verifiche automatiche: **[RELEASING.md](RELEASING.md)** · **[tests.html](https://fanza-vibes.github.io/DARTSCORE/tests.html)**

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

Se preferisci avere il file in locale, senza dipendere da internet:

👉 **[Scarica Darts_Score.html](https://github.com/Fanza-vibes/DARTSCORE/releases/latest/download/Darts_Score.html)**

Questo link scarica sempre l'ultima versione pubblicata. Salva il file dove vuoi e aprilo con un doppio clic: si apre nel browser e funziona offline, senza installare nulla.

> **Su iPhone e Android** il file finisce nell'app *File* (o nella cartella *Download*). Da lì si apre con un tocco, come qualsiasi altro documento.

Tutte le versioni, comprese le precedenti, sono nella [pagina delle Release](https://github.com/Fanza-vibes/DARTSCORE/releases).

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

**[Licenza MIT](LICENSE).** Puoi usare, modificare, ridistribuire e anche vendere DartScore, senza chiedere alcun permesso.

L'unica condizione è conservare l'avviso di copyright e il testo della licenza nelle copie. L'avviso è incluso anche in testa al file `Darts_Score.html`, così viaggia con l'app anche quando viene scaricata da sola.

Il software è fornito "così com'è", senza garanzie.

### Come citare il progetto

Il credito visibile non è un obbligo di licenza, ma è molto apprezzato. Se pubblichi una versione basata su DartScore, questa riga è pronta da copiare:

> Basato su [DartScore](https://github.com/Fanza-vibes/DARTSCORE) di Fanza-vibes, distribuito con licenza MIT.

### Contatti

Per qualsiasi domanda sul progetto:

📧 **[jackal.trail2027@eagereverest.com](mailto:jackal.trail2027@eagereverest.com)**

In alternativa puoi aprire una [issue](https://github.com/Fanza-vibes/DARTSCORE/issues) sul repository.
