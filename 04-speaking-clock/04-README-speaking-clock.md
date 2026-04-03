# Azure Speaking Clock

A Python script that uses **Azure AI Speech Services** to listen for a spoken question, recognize it, and respond with the current time — spoken aloud and saved as an audio file.

---

## What It Does

This script creates a voice-interactive clock. It listens to an audio file for the question *"What time is it?"*, determines the current time, and then **speaks the answer back** using a neural text-to-speech voice, saving the result as a `.wav` file.

| Feature | Description |
|---|---|
| **Speech Recognition** | Transcribes spoken audio from a `.wav` input file |
| **Command Matching** | Only responds if the recognized command is *"What time is it?"* |
| **Text-to-Speech** | Converts the time response into natural spoken audio |
| **Audio Output** | Saves the spoken response to `output.wav` |

---

## Prerequisites

- Python 3.7+
- An [Azure AI Speech](https://azure.microsoft.com/en-us/products/ai-services/ai-speech) resource (key + region)
- A `time.wav` audio file in the project directory containing the spoken question

---

## Installation

1. **Clone the repository** and navigate to the project folder.

2. **Install dependencies:**
   ```bash
   pip install python-dotenv azure-cognitiveservices-speech azure-core
   ```

3. **Set up your environment variables** by creating a `.env` file in the project root:
   ```env
   KEY=your_azure_speech_key
   REGION=your_azure_region (e.g. eastus)
   ```
#Note: the environment variable names must match those used in the code, optionally you can store these in Azure Key Vault (AKV) & access  using managed identity.
4. **Add your input audio file** named `time.wav` to the project directory. It should contain someone asking *"What time is it?"*

---

## Usage

```bash
python 04-speaking-clock.py
```

### Example Output

```
Ready to use speech service in: eastus
Listening...
What time is it?
Spoken output saved in output.wav
The time is 14:35
```

The spoken response will be saved to `output.wav` in the project directory.

---

## How It Works

```
time.wav (audio input)
        ↓
Speech Recognizer — transcribes the question
        ↓
Command check — is it "What time is it?"
        ↓
Get current system time
        ↓
Speech Synthesizer (en-GB-RyanNeural voice)
        ↓
output.wav (spoken time response)
```

---

## Extra Code — SSML Speech Synthesis (`04-extra_code.txt`)

The extra code file contains an **alternative version** of the speech synthesis step using **SSML (Speech Synthesis Markup Language)** instead of plain text.

### What's different?

| Feature | Main Script | Extra Code (SSML) |
|---|---|---|
| Voice | `en-GB-RyanNeural` | `en-GB-LibbyNeural` |
| Method | `speak_text_async()` | `speak_ssml_async()` |
| Control | Basic | Fine-grained (pauses, emphasis) |
| Extra content | None | Adds *"Time to end this lab!"* after the time |

### What is SSML?
SSML is an XML-based markup language that gives you precise control over how speech sounds — including pauses, pitch, rate, and voice selection. The extra code inserts a `<break strength='weak'/>` pause between the time and a closing phrase.

### How to use it
To swap in the SSML version, replace the **"Synthesize spoken output"** block in `TellTime()` with the code from `04-extra_code.txt`. Make sure `response_text` is defined before that block (it already is in the main script).

---

## Project Structure

```
.
├── 04-speaking-clock.py   # Main script
├── 04-extra_code.txt      # Optional SSML synthesis snippet
├── .env                   # Your Azure credentials (do not commit!)
├── time.wav               # Input audio file (your spoken question)
└── output.wav             # Generated output (spoken time response)
```

---

## Notes

- Never commit your `.env` file to version control. Add it to `.gitignore`.
- The script reads from a **pre-recorded** `time.wav` file — it does not use a live microphone. To use a microphone, swap `AudioConfig(filename=audioFile)` for `AudioConfig(use_default_microphone=True)`.
- The default TTS voice is `en-GB-RyanNeural`. You can browse other neural voices in the [Azure Voice Gallery](https://speech.microsoft.com/portal/voicegallery).
