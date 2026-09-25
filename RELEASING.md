# Come si rilascia una versione

Questo documento esiste perché la procedura non stia solo nella testa di chi
l'ha fatta l'ultima volta. Una parte è imposta dall'automazione, il resto
va fatto a mano nell'ordine indicato.

---

## Il principio a cui tutto risponde

**La configurazione FIGeST predefinita è il riferimento.** Qualunque modifica
al codice, anche quando riguarda solo le impostazioni personalizzate, va
verificata contro il comportamento con i valori predefiniti: non deve
cambiare, a meno che il cambiamento sia proprio l'obiettivo — e in quel caso
va confrontato con il documento ufficiale, non con l'intuizione.

Il secondo principio: **una sola fonte di verità.** Ogni informazione
duplicata prima o poi divergerà. È già successo due volte in questo progetto:
una sezione "Novità" nel README che ripeteva il CHANGELOG e si era fermata due
versioni indietro, e gli screenshot che ritraevano un calendario non più
valido.

---

## 1. Fai la modifica e verificala

**Le verifiche funzionali** stanno in [`tests.html`](tests.html). Si aprono da
un indirizzo web, non con doppio clic:

    python3 -m http.server 8000
    # poi apri http://127.0.0.1:8000/tests.html

Devono essere tutte verdi. Se hai toccato il calendario o le regole di
punteggio, questo è il controllo che conta.

**Se cambia il Referto Gara FIGeST**, la fonte da aggiornare è la costante
`REFERTO` in testa a `tests.html`, trascritta dal documento ufficiale. Poi si
adeguano `ROT_SINGOLI` e `ROT_DOPPI` nell'app finché le verifiche tornano
verdi. Mai il contrario: prima il documento, poi il codice.

> L'ordine degli incontri non è una convenzione grafica. **ART.5.3** impone di
> seguire l'ordine del referto, doppi compresi, e stabilisce che altrimenti il
> leg o il set va rigiocato.

**Se cambi i valori predefiniti** (`DEFAULT_CFG`), aggiorna anche la guida
all'uso dentro l'app. Descrive le regole predefinite, e ogni numero che cita è
marcato `data-def`: `tests.html` li confronta con i predefiniti e resta rosso
finché non coincidono. Così il workflow non può pubblicare una guida che dice
una cosa e un'app che ne fa un'altra.

---

## 2. Aggiorna la versione nei sei punti

`APP_VERSION` è la fonte, ma il numero compare in sei posti che devono
concordare. Il workflow di pubblicazione li controlla tutti e si ferma se uno
è disallineato, quindi non è una raccomandazione ma un requisito.

| # | dove | forma |
|---|---|---|
| 1 | `Darts_Score.html` — costante | `const APP_VERSION='X.Y.Z';` |
| 2 | `Darts_Score.html` — intestazione del commento | `/* DartScore vX.Y.Z` |
| 3 | `Darts_Score.html` — header della schermata iniziale | `id="app-version">vX.Y.Z` |
| 4 | `Darts_Score.html` — footer dell'informativa | `Versione X.Y.Z` |
| 5 | `CHANGELOG.md` — nuova sezione in cima | `## vX.Y.Z` |
| 6 | `README.md` — sezione Novità | `**vX.Y.Z** — …` |

I punti 3 e 4 sono sovrascritti a runtime da `init()`, quindi l'utente vedrebbe
il numero giusto comunque: si allineano perché il testo del file non menta.

**Come scegliere il numero.** Correzione o rifinitura senza effetti visibili:
terza cifra. Nuove funzionalità, o modifiche al calendario e alle regole:
seconda cifra. Non serve altro.

---

## 3. Scrivi la voce del CHANGELOG

È il testo che diventerà la descrizione pubblica della release: il workflow lo
estrae da lì, non si scrive due volte.

Va detto **cosa cambia per chi usa l'app**, non quali funzioni sono state
toccate. E quando una modifica riguarda solo le configurazioni personalizzate,
dirlo esplicitamente: chi usa i predefiniti FIGeST deve capire in una riga se
la cosa lo riguarda.

---

## 4. Rigenera gli screenshot, se serve

Le immagini in `docs/` ritraggono l'app: se hai cambiato l'interfaccia o il
calendario, sono da rifare, **compresa `og-image.png`**, che è l'anteprima
mostrata da WhatsApp e Telegram a chi riceve il link.

È l'unico punto del ciclo che nessuna automazione controlla. Se te ne
dimentichi, il README documenterà una versione dell'app che non esiste più —
è già accaduto.

---

## 5. Merge e pubblicazione

Dopo il merge su `main` basta creare il tag `vX.Y.Z`. Ci sono due strade, e in
entrambe il workflow parte da solo appena il tag esiste.

**Dall'interfaccia di GitHub**, la strada usata finora:
*Releases → Draft a new release*, poi

| campo | cosa scrivere |
|---|---|
| Choose a tag | `vX.Y.Z` → *Create new tag: vX.Y.Z on publish* |
| Target | `main` |
| Release title | `DartScore X.Y.Z` |
| Descrizione | vuota: la scrive il workflow dal CHANGELOG |
| Allegati | nessuno: lo allega il workflow |
| Set as the latest release | spuntato |

e *Publish release*. Dopo circa un minuto la release ha descrizione e allegato.

> **Controlla subito *Actions*.** Con questa strada la release viene pubblicata
> *prima* che il workflow faccia i controlli. Se il workflow diventa rosso resta
> online una release vuota, senza allegato, e siccome è la più recente il link
> di download del README smette di funzionare. In quel caso cancella la release
> e il suo tag, correggi, e ripubblica.

**Da terminale**, la strada più prudente, perché se un controllo fallisce la
release non viene creata affatto:

    git tag vX.Y.Z
    git push origin vX.Y.Z

Da qui fa tutto il workflow [`.github/workflows/release.yml`](.github/workflows/release.yml):

1. preleva il codice **a quel tag**
2. verifica i sei punti della versione e si ferma se uno non torna
3. esegue le verifiche di `tests.html` e si ferma se una fallisce
4. estrae le note dalla sezione di `CHANGELOG.md`
5. crea la release allegando `Darts_Score.html`

L'allegato è il file del repository a quel tag, non un download fatto a mano:
non può essere la versione sbagliata.

**Il nome dell'allegato deve restare `Darts_Score.html`.** Il README contiene
un link permanente a `releases/latest/download/Darts_Score.html`: cambiare il
nome lo rompe.

### Riallineare una release già pubblicata

Da *Actions → Pubblica release → Run workflow*, indicando il tag. Le note
vengono riscritte dal CHANGELOG di quel tag. Su questi rilasci il controllo
della versione si limita a due punti, perché fino alla v2.9.4 l'header statico
e il footer riportavano ancora un numero vecchio.

---

## Cosa NON fa parte del ciclo

Scelte prese consapevolmente, da non reintrodurre senza un motivo nuovo:
service worker e PWA, backend o sincronizzazione, traduzioni, build step o
divisione in moduli, storico multi-partita. Il progetto è un file HTML
singolo, senza dipendenze, che compila un referto: ogni aggiunta va misurata
contro questa frase.
