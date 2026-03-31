# Azure Text Analysis Tool

A Python code that uses **Azure AI Language Services** to automatically analyze text files and extract linguistic insights including language detection, sentiment, key phrases, and named entities.

---

## What It Does

This code scans a folder of text review files and runs each one through a series of Azure AI analyses:

| Analysis | Description |
|---|---|
| **Language Detection** | Identifies what language the text is written in |
| **Sentiment Analysis** | Determines if the tone is positive, negative, or neutral |
| **Key Phrase Extraction** | Pulls out the most important words and phrases |
| **Entity Recognition** | Identifies real-world things like people, places, and organizations |
| **Linked Entity Recognition** | Matches recognized entities to Wikipedia URLs for more context |

---

## Prerequisites

- Python 3.7+
- An [Azure AI Language](https://azure.microsoft.com/en-us/products/ai-services/ai-language) resource (endpoint + key)
- A folder named `reviews/` containing `.txt` files to analyze

---

## Installation

1. **Clone the repository** and navigate to the project folder.

2. **Install dependencies:**
   ```bash
   pip install python-dotenv azure-ai-textanalytics azure-core
   ```

3. **Set up your environment variables** by creating a `.env` file in the project root:
   ```env
   AI_SERVICE_ENDPOINT=https://<your-resource-name>.cognitiveservices.azure.com/
   AI_SERVICE_KEY=your_azure_api_key_here
   ```
#Note: the environment variable names must match those used in the code, optionally you can store these in Azure Key Vault (AKV) & access  using managed identity.
4. **Add your review files** to a folder named `reviews/` in the same directory as the  code .

---

## Usage

```bash
python 01-text-analysis.py
```

### Example Output

```
-------------
review1.txt

The hotel was wonderful. The staff were friendly and the room was spotless.

Language: English

Sentiment: positive

Key Phrases:
    hotel
    friendly staff
    spotless room

Entities
    hotel (Location)

Links
    Hotel (https://en.wikipedia.org/wiki/Hotel)
```

---

## Project Structure

```
.
├── 01-text-analysis.py   # Main code
├── .env                  # Your Azure credentials (do not commit!)
└── reviews/              # Folder of .txt files to analyze
    ├── review1.txt
    ├── review2.txt
    └── ...
```

---

