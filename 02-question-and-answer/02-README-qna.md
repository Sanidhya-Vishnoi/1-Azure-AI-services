# Azure Q&A Application

A Python script that uses **Azure AI Language Services** to power an interactive question-and-answer chatbot from the command line. Ask questions in plain English and get answers pulled from a pre-built Azure knowledge base.

---

## What It Does

This script connects to an **Azure Question Answering** project and runs an interactive loop in the terminal. You type a question, it queries your Azure knowledge base, and returns the best matched answer along with a confidence score and its source.

| Feature | Description |
|---|---|
| **Interactive Q&A Loop** | Continuously accepts questions until you type `quit` |
| **Answer Retrieval** | Fetches the best matching answer from your Azure knowledge base |
| **Confidence Score** | Shows how confident the AI is in its answer (0 to 1) |
| **Source Attribution** | Displays where the answer was pulled from |

---

## Prerequisites

- Python 3.7+
- An [Azure AI Language](https://azure.microsoft.com/en-us/products/ai-services/ai-language) resource with a **Question Answering** project deployed
- Your project name and deployment name from the Azure portal

---

## Installation

1. **Clone the repository** and navigate to the project folder.

2. **Install dependencies:**
   ```bash
   pip install python-dotenv azure-ai-language-questionanswering azure-core
   ```

#Note: the environment variable names must match those used in the code, optionally you can store these in Azure Key Vault (AKV) & access  using managed identity.
3. **Set up your environment variables** by creating a `.env` file in the project root:
   ```env
   AI_SERVICE_ENDPOINT=https://<your-resource-name>.cognitiveservices.azure.com/
   AI_SERVICE_KEY=your_azure_api_key_here
   QA_PROJECT_NAME=your_project_name
   QA_DEPLOYMENT_NAME=POC
   ```

---

## Usage

```bash
python 02-qna-app.py
```

### Example Session

```
Question:
What are your opening hours?

We are open Monday to Friday, 9am to 5pm.
Confidence: 0.9245
Source: company-faq.pdf

Question:
quit
```

> Type `quit` at any time to exit the application.

---

## Project Structure

```
.
├── 02-qna-app.py   # Main script
└── .env            # Your Azure credentials (do not commit!)
```

---
