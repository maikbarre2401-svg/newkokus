# New Kokus — Sito Web 3D 🌴

Sito web del ristorante **New Kokus** (Cucina Latinoamericana, Roma) — versione potenziata con effetti 3D.

## Com'è fatto

- `New_Kokus.dc.html` — la pagina del sito (aprila nel browser)
- `support.js` — il motore che fa funzionare la pagina (deve stare nella stessa cartella)
- `assets/` — le immagini del sito

## Effetti 3D inclusi

- **Volo 3D nella città** all'apertura: la telecamera entra in una strada latina di notte, con insegna al neon "NEW KOKUS", palme, luci e lucciole volanti
- **Parallasse col mouse** (e col **giroscopio** sul telefono): la scena si muove con te
- **Card 3D**: menù, locali e galleria si inclinano in 3D al passaggio del mouse, con riflesso di luce
- **Animazioni allo scroll**: le sezioni entrano con una rotazione 3D
- **Moneta NK rotante**, badge prezzo fluttuante, vetrina che ondeggia nella scena
- **Barra di avanzamento** in alto + header che diventa vetro scuro quando scorri
- **Bottone WhatsApp fisso** con effetto pulsazione

Tutto il resto funziona come prima: **menù modificabile** (✎ Gestione menù, si salva sul dispositivo) e **prenotazioni via WhatsApp**.

## Le tue foto

Le immagini in `assets/` sono **segnaposto**: sostituiscile con le tue foto vere usando **gli stessi nomi file**:

| File | Cosa metterci |
|---|---|
| `storefront.png` | La vetrina del locale (verticale, ~480×854) |
| `storefront-night.png` | Il locale di sera |
| `interior.png` | La sala interna |
| `arepas.png` | Foto delle arepas |
| `desayunos.png` | I desayunos latinos |
| `terrazza.png` | La Terrazza del Kokus |
| `combo.png` | Il Combo 3 (verticale) |
| `menudia.png` | Il menù del día |

## Il percorso 3D "Come arrivare" 🚶🌴

La sezione **Come arrivare** è un percorso animato in 3D a 9 tappe: la telecamera vola di foto in foto dalla Metro Cornelia fino alla porta del New Kokus 2 (premi ▶ oppure usa frecce e numeri).

Anche qui le immagini sono segnaposto numerati: salva le tue 9 foto del percorso (le schermate di Street View che hai già) in `assets/` con questi nomi, **nello stesso ordine**:

| File | La tua foto |
|---|---|
| `percorso-1.png` | Mappa / Metro A Cornelia (Circonvallazione Cornelia) |
| `percorso-2.png` | Attraversamento al semaforo — Circonvallazione Cornelia 104 |
| `percorso-3.png` | Via di Boccea 114 — marciapiede Intersport/Cisalfa |
| `percorso-4.png` | Via di Boccea 139 — incrocio con Kiko |
| `percorso-5.png` | Via Federico Galeotti 2 — inizio della via |
| `percorso-6.png` | Via Federico Galeotti 26 — prosegui dritto |
| `percorso-7.png` | Via Federico Galeotti 30 — angolo con Via G. Tamassia |
| `percorso-8.png` | Via Giovanni Tamassia 42 — quasi arrivato |
| `percorso-9.png` | Via Giovanni Tamassia 32 — la vetrina del New Kokus 2! |

Consiglio: ritaglia le schermate togliendo la barra di ricerca e i pannelli di Google prima di salvarle (e ancora meglio: foto scattate da te, le schermate di Google Maps contengono contenuti © Google).

## Come aprirlo

Doppio click su `New_Kokus.dc.html` (serve internet la prima volta per i caratteri e la libreria grafica).

## Come metterlo ONLINE (gratis, 2 minuti) 🌐

Il modo più facile è **Netlify Drop** — non serve saper programmare:

1. Vai su **https://app.netlify.com/drop**
2. **Trascina l'intera cartella `new-kokus`** dentro la pagina
3. Fine! Ti dà subito un indirizzo tipo `https://nome-a-caso.netlify.app` da condividere su WhatsApp e Instagram
4. (Facoltativo) Registrandoti gratis puoi cambiare il nome, es. `newkokus.netlify.app`, o collegare un dominio tuo tipo `newkokus.it`

Alternative che funzionano uguale: **Vercel** (vercel.com), **GitHub Pages**, o qualsiasi hosting — basta caricare la cartella così com'è (c'è già `index.html` che fa da porta d'ingresso).

⚠️ Prima di pubblicare ricordati di mettere le **foto vere** in `assets/` (vedi le tabelle sopra), così il sito esce già bello pronto.

## SEO già incluso ✅

- Titolo e descrizione per Google
- Anteprima social (Open Graph): quando condividi il link su WhatsApp/Facebook esce foto + titolo
- Scheda ristorante (dati strutturati schema.org) con indirizzi, telefono e orari dei due locali
- Favicon 🌴
