#Azure Custom Text Classifier

A Python script that uses **Azure AI Language Services** to automatically classify text files into custom categories using a trained machine learning model.

---

## What It Does

This script reads a batch of articles from a folder and sends them all at once to an **Azure Custom Text Classification** model. Each file is assigned a category with a confidence score, making it easy to sort and organize large volumes of text automatically.

| Feature | Description |
|---|---|
| **Batch Processing** | Reads and classifies all files in the `articles/` folder in one go |
| **Single-Label Classification** | Assigns each document to one best-matching category |
| **Confidence Scoring** | Shows how confident the model is in each classification (0 to 1) |
| **Error Reporting** | Clearly reports any files that failed to classify and why |

---

## Prerequisites

- Python 3.7+
- An [Azure AI Language](https://azure.microsoft.com/en-us/products/ai-services/ai-language) resource with a **Custom Text Classification** project trained and deployed
- Your project name and deployment name from Azure Language Studio

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
   PROJECT=your_project_name
   DEPLOYMENT=your_deployment_name
   ```
#Note: the environment variable names must match those used in the code, optionally you can store these in Azure Key Vault (AKV) & access  using managed identity.

4. **Add your article files** to a folder named `articles/` in the same directory as the script.

---

## Usage

```bash
python 03-classify-text.py
```

### Example Output

```
article1.txt was classified as 'Sports' with confidence score 0.98.
article2.txt was classified as 'Technology' with confidence score 0.87.
article3.txt was classified as 'Politics' with confidence score 0.76.
article4.txt has an error with code 'InvalidDocument' and message 'Document is empty.'
```

---

## Project Structure

```
.
├── 03-classify-text.py   # Main script
├── .env                  # Your Azure credentials (do not commit!)
└── articles/             # Folder of .txt files to classify
    ├── article1.txt
    ├── article2.txt
    └── ...
```

---

## How It Differs from Text Analysis (01-text-analysis.py)

| Feature | Text Analysis | Text Classifier |
|---|---|---|
| Processing | One file at a time | All files batched together |
| Output | Language, sentiment, phrases, entities | Category label + confidence |
| Model type | Pre-built Azure models | Your own custom trained model |
| Use case | General text insights | Sorting/organizing documents |

---

## Notes

- Never commit your `.env` file to version control. Add it to `.gitignore`.
- The custom classification model must be **trained and deployed** in [Azure Language Studio](https://language.cognitive.azure.com/) before running this script.
- A confidence score closer to **1.0** means a stronger category match. Consider setting a minimum threshold (e.g. 0.7) for production use.
- All text files in the `articles/` folder must be UTF-8 encoded.
