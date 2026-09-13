# Asta Fantacalcio

Web app singola pagina per gestire l'asta del fantacalcio. Nessun database, nessun server: tutto sta in un file HTML e i dati si salvano nel browser.

## Cosa fa

- Da 2 a 10 squadre, ognuna parte con **500 crediti** e deve riempire **3 P / 8 D / 8 C / 6 A**.
- Carica il file `.xlsx` delle quotazioni Fantacalcio.it (usa la colonna **Qt.A**).
- Lista giocatori divisa per ruolo, ordinata dalla quotazione più alta.
- Click su un giocatore → modale con prezzo di aggiudicazione e squadra.
- Vincolo automatico: il prezzo massimo tiene sempre 1 credito libero per ogni slot ancora da riempire.
- Vista squadre in **striscia scorrevole** oppure **panoramica** compatta.
- **Annulla** l'ultima assegnazione, rimuovi un giocatore da una squadra, esporta/importa il JSON di backup.

## Come si usa

1. Apri `index.html` (con Chrome, Safari, Firefox — desktop o mobile).
2. **Setup**: scegli il numero di squadre, dai i nomi, carica il file Excel delle quotazioni.
3. Al click su "Inizia asta" parte la gestione.
4. Durante l'asta:
   - Tab **Giocatori**: trova quello messo all'asta (per ruolo o con la ricerca), tocca, inserisci prezzo, scegli squadra, conferma.
   - Tab **Squadre**: vedi tutte le rose. In "Dettaglio" scorri a destra tra le squadre, in "Panoramica" le vedi tutte insieme e tocchi quella che ti interessa per zoomare.
   - Bottone **Annulla** in alto per rimediare a un errore.
5. I dati sono salvati automaticamente nel browser. Riapri la pagina e trovi l'asta come l'avevi lasciata.

### Consigli d'uso

- Da **Impostazioni** puoi rinominare le squadre in qualsiasi momento.
- Prima di iniziare, esporta il JSON come backup (o dopo ogni sessione lunga). Serve anche se vuoi continuare l'asta su un altro dispositivo (importi il JSON e riprendi).
- Se una squadra ha rosa completa, la vedrai marcata come "Rosa completa ✓" nella card.

## Pubblicare su GitHub Pages (per averla sul telefono)

Serve un account GitHub. Se non ce l'hai, iscriviti gratis su [github.com](https://github.com).

1. Su GitHub, crea un nuovo repo. Nome per esempio `asta-fantacalcio`, puoi lasciarlo **pubblico** (per GitHub Pages gratis il repo deve essere pubblico, ma il link è sconosciuto a chi non lo cerca).
2. Carica **solo il file `index.html`** (bottone "Add file" → "Upload files", trascina, commit).
3. Vai su **Settings → Pages** del repo.
4. Sotto "Build and deployment", "Source" scegli **Deploy from a branch**, branch **main**, cartella **/root**. Salva.
5. Aspetta 1-2 minuti. In cima alla stessa pagina apparirà l'URL, tipo:
   ```
   https://tuo-username.github.io/asta-fantacalcio/
   ```
6. Apri quell'URL dal telefono. Su Chrome Android: menu **⋮ → Aggiungi a schermata Home** per averla come icona.

### Alternativa rapida senza GitHub

Se non vuoi creare un repo: vai su [app.netlify.com/drop](https://app.netlify.com/drop), trascina la cartella `ASTA FANTACALCIO`, ottieni subito un URL pubblico. Gratis, zero configurazione.

## Note tecniche

- Un solo file, tutto embedded (HTML + CSS + JS).
- Parsing Excel via [SheetJS](https://sheetjs.com) caricato da CDN (`cdn.jsdelivr.net`). Serve internet solo al primo caricamento della pagina, poi il browser lo mette in cache.
- Persistenza in `localStorage` sotto la chiave `asta_fantacalcio_v1`. Dati legati al browser + dispositivo: se cambi telefono, esporta/importa il JSON.
- Nessuna dipendenza da installare, nessun build step.

## Aggiungere / cambiare cose

Il file `index.html` è commentato in italiano ed è organizzato in sezioni chiare (Costanti, Stato, Persistenza, Parsing Excel, Rendering, Modale, Handlers, Bootstrap). Se ti serve una modifica veloce (nomi campi, colori, limiti) sai dove mettere le mani.
