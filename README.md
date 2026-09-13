# Asta Fantacalcio

Web app singola pagina per gestire l'asta del fantacalcio. Nessun database, nessun server: tutto sta in un file HTML e i dati si salvano nel browser.

## Cosa fa

- **Più aste in parallelo** — ognuna con le sue squadre, i suoi crediti e la sua lista giocatori.
- Numero squadre libero (minimo 2, nessun tetto).
- Crediti per squadra **configurabili** (default 500), da 25 in su.
- Ogni squadra deve riempire **3 P / 8 D / 8 C / 6 A**.
- Carica il file `.xlsx` delle quotazioni Fantacalcio.it (usa la colonna **Qt.A**).
- Lista giocatori divisa per ruolo, ordinata dalla quotazione più alta.
- Click su un giocatore → modale con prezzo di aggiudicazione e squadra.
- Vincolo automatico: il prezzo massimo tiene sempre 1 credito libero per ogni slot ancora da riempire.
- Vista squadre in **striscia scorrevole** oppure **panoramica** compatta.
- **Annulla** l'ultima assegnazione, rimuovi un giocatore da una squadra, esporta/importa il JSON di backup.

## Come si usa

1. Apri `index.html` (con Chrome, Safari, Firefox — desktop o mobile).
2. **Setup della prima asta**: dai un nome, scegli numero squadre e crediti, dai i nomi alle squadre, carica il file Excel delle quotazioni.
3. Al click su "Inizia asta" parte la gestione.
4. Durante l'asta:
   - Tab **Giocatori**: trova quello messo all'asta (per ruolo o con la ricerca), tocca, inserisci prezzo, scegli squadra, conferma.
   - Tab **Squadre**: vedi tutte le rose. In "Dettaglio" scorri a destra tra le squadre, in "Panoramica" le vedi tutte insieme e tocchi quella che ti interessa per zoomare.
   - Bottone **Annulla** in alto per rimediare a un errore.
5. I dati sono salvati automaticamente nel browser. Riapri la pagina e trovi l'asta come l'avevi lasciata.

### Gestire più aste

- In alto, accanto al titolo, c'è un **selettore asta**: clicchi per switchare fra aste, creare una **nuova asta**, o andare in "Gestisci aste".
- **Nuova asta** puoi partire da zero con un nuovo file Excel, oppure **riusare la lista giocatori** dell'asta corrente (utile per rifare l'asta con la stessa lista).
- Da **Impostazioni → Le mie aste** rinomini, duplichi, apri o elimini un'asta. Ne deve restare sempre almeno una.

### Consigli d'uso

- Prima di iniziare, esporta il JSON come backup. Serve anche se vuoi continuare l'asta su un altro dispositivo (importi il JSON e riprendi).
- Se una squadra ha rosa completa, la vedrai marcata come "Rosa completa ✓" nella card.
- Il backup JSON contiene **tutte** le aste. All'import puoi scegliere se sostituire tutto o aggiungere le aste importate.

## Pubblicare su GitHub Pages (per averla sul telefono)

Vedi il repo `Prestigiooo90/ASTA-FANTACALCIO` su GitHub — il flusso è: apri GitHub Desktop, fai commit dei cambiamenti, push. GitHub Pages si aggiorna da solo in ~1 minuto.

URL live: https://prestigiooo90.github.io/ASTA-FANTACALCIO/

Sul telefono: apri l'URL con Chrome/Safari → menu → **Aggiungi a schermata Home**. Diventa un'icona come un'app.

## Note tecniche

- Un solo file, tutto embedded (HTML + CSS + JS).
- Parsing Excel via [SheetJS](https://sheetjs.com) caricato da CDN.
- Persistenza in `localStorage` sotto la chiave `asta_fantacalcio_v1`. Contiene **tutte** le aste in formato v2 (struttura `{ auctions: { id: {…} } }`). I dati salvati con la versione precedente (asta singola) vengono migrati automaticamente in un'asta chiamata "Asta principale".
- Nessuna dipendenza da installare, nessun build step.

## Aggiungere / cambiare cose

Il file `index.html` è commentato in italiano ed è organizzato in sezioni chiare (Costanti, Stato, Persistenza + migrazione, Helper aste, Parsing Excel, Rendering, Modali, Handlers, Bootstrap).
