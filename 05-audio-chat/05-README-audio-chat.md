# Azure Audio Chat

A Python script that uses **Azure AI Projects** and **OpenAI** to let you ask questions about an audio file in natural language. It downloads an MP3, encodes it, and sends it alongside your question to a multimodal AI model for a response.

---

## What It Does

This script creates an interactive chat loop where you can ask questions about the contents of an audio file. The AI listens to the audio and answers your questions based on what it hears — no manual transcription needed.

| Feature | Description |
|---|---|
| **Audio Understanding** | Sends an MP3 file directly to the AI model for comprehension |
| **Interactive Q&A Loop** | Continuously accepts questions until you type `quit` |
| **Multimodal Input** | Combines your text question with audio content in a single request |
| **Azure AI Projects** | Uses Azure's project client to connect to a deployed OpenAI model |

---

## Prerequisites

- Python 3.7+
- An [Azure AI Foundry](https://ai.azure.com/) project with a **multimodal OpenAI model** deployed (e.g. `gpt-4o`)
- Your project endpoint and deployment name

---

## Installation

1. **Clone the repository** and navigate to the project folder.

2. **Install dependencies:**
   ```bash
   pip install python-dotenv azure-identity azure-ai-projects openai requests
   ```

3. **Set up your environment variables** by creating a `.env` file in the project root:
   ```env
   PROJECT_ENDPOINT=https://<your-project>.services.ai.azure.com/api/projects/<your-project-name>
   MODEL_DEPLOYMENT=your_model_deployment_name
   ```
   #Note: the environment variable names must match those used in the code, optionally you can store these in Azure Key Vault (AKV) & access  using managed identity.


---

## Usage

```bash
python 05-audio-chat.py
```

### Example Session

```
Ask a question about the audio
(or type 'quit' to exit)
What topics are discussed in the audio?

Getting a response ...

The audio discusses the supply and pricing of avocados, including seasonal availability and bulk ordering options.

Ask a question about the audio
(or type 'quit' to exit)
quit
```

---

## How It Works

```
User types a question
        ↓
Script downloads avocados.mp3 from GitHub
        ↓
Audio is base64-encoded
        ↓
Question + encoded audio sent to Azure OpenAI model
        ↓
Model listens to the audio and answers the question
        ↓
Response printed to the console
```

---

## How It Differs from Previous Scripts

| Feature | Speaking Clock (04) | Audio Chat (05) |
|---|---|---|
| Audio direction | Output (text → speech) | Input (audio → understanding) |
| Azure service | Azure Speech SDK | Azure AI Projects + OpenAI |
| Interaction | Command matching | Open-ended Q&A |
| Audio source | Local `.wav` file | Remote `.mp3` from URL |

---

## Project Structure

```
.
├── 05-audio-chat.py   # Main script
└── .env               # Your Azure credentials (do not commit!)
```

> The audio file (`avocados.mp3`) is fetched directly from GitHub at runtime — no local audio file is needed.

---

## Notes

- Never commit your `.env` file to version control. Add it to `.gitignore`.
- The model must support **multimodal / audio input**. Standard text-only models will not work — use a deployment like `gpt-4o`.
- The audio file is re-downloaded and re-encoded on **every question** in the loop. For production use, consider caching the encoded audio outside the loop.
- Authentication uses `DefaultAzureCredential` with environment and managed identity excluded — you may need to be logged in via the **Azure CLI** (`az login`) for this to work locally.
