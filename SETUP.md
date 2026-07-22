# SMS en Français — Setup

A texting app that runs entirely on your computer and talks to a **free, local AI model** via Ollama. No API keys, no subscriptions, no per-message cost.

## 1. Install Ollama
Download and install from **https://ollama.com** (Mac, Windows, or Linux).

## 2. Pull a model
Open a terminal and run one of these (first pull downloads the model, a few GB):

```
ollama pull llama3.1
```

Other good options for French: `mistral`, `qwen2.5:7b` (qwen2.5 is particularly strong at multilingual/French).

## 3. Start Ollama with browser access enabled
By default Ollama only accepts requests from a couple of origins. To let this app talk to it, start it like this:

**Mac/Linux:**
```
OLLAMA_ORIGINS="*" ollama serve
```

**Windows (PowerShell):**
```
$env:OLLAMA_ORIGINS="*"; ollama serve
```

If Ollama is already running as a background service, quit it first (check your menu bar / system tray) so this command can take over on port 11434.

## 4. Run the app
The app is a single `index.html` file, but for the browser to load fonts/fetch correctly, serve it from a local web server instead of double-clicking it:

```
cd path/to/french-texting-app
python3 -m http.server 8000
```

Then open **http://localhost:8000** in your browser.

## 5. First-time setup in the app
Tap the gear icon (top right) and check:
- **Ollama address**: `http://localhost:11434`
- **Model**: match whatever you pulled, e.g. `llama3.1`
- It'll show a green "✓ Connecté" if everything's wired up correctly.

From there, set your level (A1–C1), tu/vous, and a conversation topic or persona (e.g. "Amélie, a Parisian barista" or "Léo, your chatty college friend"), then just start texting in French.

## How it works
- Every message you send gets checked for grammar/spelling mistakes, shown as a small "correction receipt" between messages.
- Each AI reply has a tappable "Voir la traduction" link to reveal the English translation.
- Everything (settings + chat history) is saved locally in your browser — nothing goes to any external server.

## Troubleshooting
- **Red "✗" in connection check**: make sure `ollama serve` is running with `OLLAMA_ORIGINS="*"` set, and that you pulled the model listed in Settings.
- **Replies aren't valid French / correction card looks empty**: smaller models sometimes don't follow the JSON format perfectly. Try `qwen2.5:7b` or `llama3.1` — they're both reliable at this. If a model can't run on your hardware, try a smaller quantized version, e.g. `llama3.1:8b-instruct-q4_0`.
- **Slow replies**: local model speed depends on your CPU/GPU. Smaller models (7-8B) are the sweet spot for most laptops.
