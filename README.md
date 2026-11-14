# Transcribe Speech – Lokale Transkription mit whisper.cpp

Dieses Projekt zeigt, wie du **Videos oder Audiodateien** auf deinem eigenen Rechner mithilfe von **whisper.cpp** in Text umwandelst. Alles läuft komplett lokal – keine API‑Keys, keine Upload‑Limits und keine Datenschutz‑Bedenken.

## Was du brauchst

| Programm | Wie du es installierst (macOS) |
|----------|--------------------------------|
| **ffmpeg** | `brew install ffmpeg` |
| **whisper‑cpp** (oder `whisper-cli` bei Homebrew) | `brew install whisper-cpp` |
| **Whisper‑Modell** | ```bash
curl -o ggml-large-v3-q5_0.bin -L "https://huggingface.co/ggerganov/whisper.cpp/resolve/main/ggml-large-v3-q5_0.bin?download=true"
``` |

> **Hinweis:** Das Modell ist ca. 1 GB groß. Auf GitHub wird es über **Git LFS** verwaltet, damit das Repository nicht zu groß wird.

## Schritt‑für‑Schritt‑Anleitung

1. **Audio‑Datei vorbereiten** – Du kannst ein Video, ein MP3, eine M4A‑Datei oder jede andere Audiospur verwenden.
2. **In das von Whisper erwartete Format umwandeln** (16 kHz, Mono, WAV):
   ```bash
   ffmpeg -i DEINE_DATEI.ext -ar 16000 -ac 1 input.wav
   ```
   *`DEINE_DATEI.ext`* ist dabei dein Originalfile, z. B. `mein‑video.mp4`.
3. **Transkribieren**:
   ```bash
   whisper-cpp -m ggml-large-v3-q5_0.bin input.wav --output-txt
   ```
   (Falls das Homebrew‑Binary `whisper-cli` heißt, verwende stattdessen `whisper-cli`.)
   - Die Ausgabe wird in **`input.txt`** gespeichert und zusätzlich im Terminal angezeigt.
4. **Optional: Untertitel‑Formate erzeugen**
   - SRT (häufig für Video‑Player):
     ```bash
     whisper-cpp -m ggml-large-v3-q5_0.bin input.wav --output-srt
     ```
   - VTT (für Web‑Player):
     ```bash
     whisper-cpp -m ggml-large-v3-q5_0.bin input.wav --output-vtt
     ```
5. **Ergebnis ansehen** – Öffne `input.txt` (z. B. `open -a TextEdit input.txt` oder `cat input.txt`).

## Was das Projekt enthält
- Das Whisper‑Modell **`ggml-large-v3-q5_0.bin`** (via Git LFS)
- Eine Beispiel‑Audiodatei (`input.wav`)
- Das resultierende Transkript (`input.txt`)
- Die Datei `Transcript_Test.mov` (ein kurzes Test‑Video)
- Dieses `README.md` mit einer einfachen Anleitung für Einsteiger.

## Weiterführende Ideen
- **Übersetzung**: Füge das Flag `--translate` hinzu, um gesprochene Sprache in Englisch zu übersetzen.
- **Andere Modellgrößen**: Experimentiere mit kleineren Modellen, wenn du weniger Speicher hast (z. B. `ggml-tiny.bin`).
- **Batch‑Verarbeitung**: Schreibe ein kurzes Shell‑Script, das einen ganzen Ordner mit Audiodateien automatisch transkribiert.

Viel Spaß beim Transkribieren! 🎤📝