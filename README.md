# MAIK — assistente AI personale

Due modi di usare MAIK, scegli quello che preferisci:

| | **`index.html`** (client) | **`maik_server.py`** (server) |
|---|---|---|
| Avvio | apri il file nel browser | `python maik_server.py` |
| Dipendenze | nessuna | nessuna (solo stdlib Python) |
| Memoria | nel browser (`localStorage`) | su disco in `dati_maik/*.json` |
| Ideale per | uso veloce su un solo dispositivo | memoria persistente e robusta |

Entrambi parlano con un modello locale tramite **Ollama** e rispondono in **streaming**.

## Quali modelli Ollama usare

MAIK usa due modelli: uno per **chattare/ragionare** e uno **multimodale per la webcam** (👁️ Guarda). Scegli in base al tuo PC:

| Il tuo PC | Chat / ragionamento | Visione (webcam) |
|---|---|---|
| 💪 Potente (≥16 GB RAM o GPU) | `qwen2.5:14b` (o `llama3.1:8b`) | `llava:13b` |
| ⚖️ Medio (8–12 GB) | `llama3.1` | `llava` |
| 🪶 Leggero (≤8 GB) | `llama3.2:3b` | `moondream` |

```bash
ollama pull llama3.1     # chat
ollama pull llava        # visione (per far "vedere" MAIK) — compatibile ovunque
```

- Nel **client** (`index.html`): scegli il modello chat e quello visione in **⚙ Impostazioni**.
- Nel **server** (`maik_server.py`): variabili d'ambiente `MAIK_MODELLO` (chat) e `MAIK_MODELLO_VISIONE` (webcam).
- In ogni caso MAIK **prova più modelli visione in cascata** (quello scelto → `llava` → `moondream`), quindi se ne hai almeno uno installato funziona.

> ⚠️ **Errore `unknown model architecture: 'mllama'`** con `llama3.2-vision`?
> Vuol dire che il tuo **Ollama è troppo vecchio** (serve ≥ 0.4). Due soluzioni:
> 1. **Più semplice:** usa `llava` →  `ollama pull llava`
> 2. Aggiorna Ollama all'ultima versione da <https://ollama.com/download>
>
> `llava` e `moondream` funzionano su praticamente tutte le versioni di Ollama.

---

## MAIK // CORE V7.0 — `index.html`

Assistente AI personale in un **singolo file HTML**. Nessuna installazione, nessun build: apri `index.html` nel browser e funziona. Si connette a un modello locale tramite **Ollama** e ricorda tutto in `localStorage`.

## Avvio rapido

1. Apri `index.html` nel browser (doppio click, oppure servilo con `python3 -m http.server`).
2. (Opzionale ma consigliato) avvia Ollama per le risposte AI complete:
   ```bash
   ollama serve
   ollama pull llama3.2        # o un altro modello a tua scelta
   ```
3. In MAIK apri **⚙ Impostazioni** → scegli il modello rilevato → **Salva**.

Senza Ollama, MAIK funziona comunque in modalità offline (memoria, profilo, meteo, promemoria, voce).

## Novità rispetto alla V6.0

- **Risposte in streaming** token-per-token, con pulsante **■ Stop**.
- **Auto-rilevamento dei modelli** installati su Ollama (niente più nome hardcoded) + selettore nelle impostazioni.
- **Pannello Impostazioni**: URL Ollama, modello, persona/personalità, creatività (temperature), TTS on/off, scelta voce, ascolto continuo, colore accento.
- **Memoria strutturata**: fatti, gusti (mi piace / non mi piace), profilo, persone, obiettivi e **promemoria** — tutto iniettato nel prompt.
- **Estrazione automatica** di nome, età, città, lavoro, gusti, insegnamenti e promemoria dalle frasi.
- **Cronologia conversazione persistente**: riapri MAIK e ritrovi la chat.
- **Rendering Markdown** nelle risposte (grassetto, elenchi, codice, link).
- **Rilevamento volto reale** via `FaceDetector` API dove disponibile (fallback simulato altrove).
- **Backup**: esporta/importa tutti i dati in JSON.
- **Analisi emozioni** più ricca con barra d'intensità.
- **Riconoscimento vocale** con risultati intermedi e modalità ascolto continuo.
- Layout **responsive** per mobile e migliorie di robustezza/errore.

### Sfera 3D + Strumenti (ultimo aggiornamento)

- 🔮 **Nuova sfera 3D**: nuvola di punti che **ruota di continuo** (animata anche da ferma), con nucleo pulsante e barre quando "parla". Cambia colore in base allo stato (idle / pensa / parla / volto rilevato). Ora **si ridimensiona da sola** in base allo spazio: niente più sfera bloccata in un angolo su mobile. La puoi trascinare, bloccare (📌) e ricentrare.
- 🧰 **Pannello Strumenti** (pulsante in alto) con 12 utility:

  | | | |
  |---|---|---|
  | 🧮 Calcolatrice | ⏱️ Timer/Pomodoro | ⏲️ Cronometro |
  | 🎲 Random (dado/moneta/numero) | 🔄 Convertitore (lunghezza, peso, volume, temperatura) | 🌍 Orologi mondiali |
  | 📝 Note rapide | 🔑 Generatore password | 🌐 Traduttore (AI) |
  | 📋 Riassumi testo (AI) | 🔢 Conta parole/caratteri | 🎯 Scegli per me |

  Le utility funzionano **offline**; *Traduttore* e *Riassumi* usano il modello Ollama.

### 🫂 Modalità Amico (compagnia)

Pulsante **🫂 AMICO** in alto: trasforma MAIK in un compagno che **ti vede e ti parla** come un amico vero.

- 📷 **Ti vede davvero**: accende la webcam e rileva la tua **presenza reale** — `FaceDetector` nativo dove c'è, altrimenti rilevamento del **movimento** (differenza tra fotogrammi). Niente più rilevamento finto a caso.
- 👋 **Ti accoglie quando torni**: se sparisci e poi riappari, ti saluta ("Bentornato! Mi eri mancato 😊").
- 🎙️ **Ascolto continuo a mani libere**: parli e MAIK risponde a voce; mentre parla mette in pausa il microfono per non sentirsi da solo, poi riapre le orecchie.
- 💬 **Inizia lui la conversazione**: quando c'è silenzio (ogni ~1–2 min) MAIK ti scrive/parla spontaneamente, usando il contesto (nome, ora, promemoria, obiettivi, meteo). Se Ollama è online a volte genera lui la frase, altrimenti usa frasi calorose pronte.
- 🔊 La voce (TTS) si attiva da sola in questa modalità.

> La webcam e il microfono partono al **click** sul pulsante (richiesto dai browser) e funzionano su `localhost`/HTTPS. Tutto resta in locale.

## Privacy

Tutti i dati restano nel tuo browser (`localStorage`). Le uniche chiamate di rete sono: Ollama (in locale) e `wttr.in` per il meteo.

---

## MAIK — Server V6.0 — `maik_server.py`

Server in **puro Python (solo libreria standard, niente pip)** con memoria avanzata salvata su disco. Serve la GUI nel browser e fa da ponte verso Ollama.

```bash
ollama pull llama3.1      # una volta
python maik_server.py     # si apre da solo nel browser su :8137
```

Se nella stessa cartella c'è il tuo `aria.html`, il server usa quella interfaccia 3D; altrimenti parte con una **GUI integrata** completa — **sfera 3D animata + chat in streaming + pannello 🧰 strumenti + 🫂 Modalità Amico + 👁️ visione webcam** — collegata agli endpoint del server, così la memoria viene salvata **su disco** (non nel browser). Funziona out-of-the-box senza `aria.html`.

Anche il server ha la **🫂 Modalità Amico** (ti vede, ti ascolta e ti parla) e il pulsante **👁️ Guarda**: cattura un fotogramma dalla webcam e lo manda al modello multimodale (`MAIK_MODELLO_VISIONE`) tramite il nuovo endpoint `POST /vedi`, e MAIK descrive cosa vede.

### Novità V6.0 rispetto a v5.0

- ⚡ **Risposte in streaming** token-per-token (`POST /chat/stream`, SSE) — niente più attese mute.
- 🔒 **Memoria a prova di crash**: scritture atomiche (`.tmp` + `os.replace`) e **lock multi-thread**, niente JSON corrotti con richieste in parallelo.
- 📁 Tutti i dati in una **cartella dedicata** `dati_maik/`, con **migrazione automatica** dai vecchi file di v5.0.
- ⚙️ **Configurabile da variabili d'ambiente**: `MAIK_MODELLO`, `MAIK_PORTA`, `MAIK_OLLAMA`, `MAIK_DATA`, `MAIK_HOST`, `MAIK_NOME`.
- 🐛 **Bug-fix estrattore nomi**: *"sono stanco"* non viene più salvato come nome "Stanco".
- 🩺 Nuovi endpoint `GET /salute` e `GET /config`; chiamate a Ollama più robuste con errori chiari.

Eredita da v5.0: profilo ricco, memoria episodica, timeline, umore tracker, ricerca, obiettivi/sogni, relazioni, reset selettivo, statistiche.

### Esempio configurazione

```bash
MAIK_MODELLO=llama3.2 MAIK_PORTA=9000 python maik_server.py
```

## Frasi che MAIK impara da solo

- `Mi chiamo Maik` → salva il nome
- `Ho 28 anni` → salva l'età
- `Vivo a Roma` → salva la città
- `Mi piace la pizza` / `Odio il traffico` → salva i gusti
- `Ti insegno che ...` → memorizza un fatto
- `Ricordami di chiamare il dottore domani alle 9` → crea un promemoria
