# AI Voice Note Pro

Streamlit app to record or upload audio, transcribe it with Whisper, and generate a structured summary (optionally using the OpenAI API).

## Features

- Record audio (microphone) or upload audio files
- Multilingual transcription (auto-detect or pick a language)
- Optional "Translate to English" transcription task (Whisper)
- Structured summarization
  - Uses OpenAI API if `OPENAI_API_KEY` is configured
  - Falls back to a local heuristic summarizer if not
- Text-to-speech playback of the generated summary
- Export transcription (`.txt`) and summary (`.md`)

## Requirements

- Python 3.10+ recommended
- FFmpeg available on your system `PATH` (needed by Whisper / audio decoding)
- A working microphone (for the Record tab)

Python dependencies are listed in `requirements.txt`.

## Quick Start (Windows PowerShell)

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Create a local `.env` file (do not commit it) to enable OpenAI summaries:

```env
OPENAI_API_KEY=your_key_here
```

Run the app:

```powershell
streamlit run main_app.py
```

Alternative:

```powershell
python run.py
```

## How To Use

1. Open the sidebar and click "Load Model" (Whisper model size: `tiny/base/small/medium`).
2. Choose:
   - `Transcription language`: `Auto-detect` (recommended) or a specific language.
   - `Task`: `Transcribe (original language)` or `Translate to English`.
3. Record audio or upload a file, then transcribe.
4. Go to Summary and click "Generate Summary".
5. Use Export to download transcription/summary.

## Project Layout

- `main_app.py`: Streamlit app entrypoint
- `run.py`: Convenience runner
- `src/core/transcribe.py`: Whisper transcription engine (supports `language` and `task`)
- `src/core/summarize.py`: Summary engine (OpenAI-backed when configured, otherwise local)
- `src/core/audio_recorder.py`: Microphone recording utilities
- `src/core/tts_engine.py`: Text-to-speech utilities
- `tests/`: Test files (if present)

## Notes / Troubleshooting

- If transcription fails on uploads, install FFmpeg and ensure `ffmpeg` is on your `PATH`.
- If OpenAI summarization fails or you do not set `OPENAI_API_KEY`, the app will summarize locally.
- Large audio files can take time to transcribe depending on your CPU and model size.

## Security

- Never commit `.env` or API keys to GitHub.
- If you accidentally committed a key at any point, rotate/revoke it immediately.

