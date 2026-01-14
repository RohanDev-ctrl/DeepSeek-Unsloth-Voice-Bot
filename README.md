# DeepSeek-Unsloth-Voice-Bot
A fine-tuning and inference pipeline for banking intent detection using DeepSeek-7b, Unsloth, and Twilio voice automation.

# 🏦 DeepSeek Banking Recovery Agent

> **Project Status:** Active | **Model:** DeepSeek-7b | **Pipeline:** Unsloth, Twilio, AssemblyAI, Google Sheets

An end-to-end AI automation pipeline for debt collection and banking recovery. This project demonstrates how to fine-tune **DeepSeek-7b** (using Unsloth) to recognize banking intents and integrates it with **Twilio**, **AssemblyAI**, and **Google Sheets** for fully automated voice calls.

---

## 🚀 Project Overview

This repository contains a unified Jupyter Notebook that performs three key functions:

1.  **Fine-Tuning:** Trains a custom LLM on banking scenarios (e.g., "Promise to Pay", "Financial Hardship", "Refusal").
2.  **Voice Automation:** Automatically calls customers from a Google Sheet using Twilio.
3.  **Real-Time Analytics:** Transcribes calls using AssemblyAI, analyzes the customer's intent using the fine-tuned model, and updates the database (Google Sheets) instantly.

---

## ⚙️ Architecture

The workflow follows this cycle:

1.  **Trigger:** Script reads customer data (Name, Phone, Due Date) from **Google Sheets**.
2.  **Action:** **Twilio** initiates a voice call and records the customer's response.
3.  **Process:** **AssemblyAI** transcribes the audio recording to text.
4.  **Intelligence:** The fine-tuned **DeepSeek** model analyzes the text to determine the intent (e.g., *"User promised to pay on the 15th"*).
5.  **Result:** The intent status is written back to **Google Sheets** for the collections team.

---

## 🛠️ Tech Stack

* **Model:** `DeepSeek-LLM-7b-Base`
* **Fine-Tuning:** `Unsloth` (LoRA adapters for efficient training)
* **Voice Telephony:** Twilio Voice API
* **Speech-to-Text:** AssemblyAI
* **Database:** Google Sheets API
* **Environment:** Google Colab (Recommended for GPU access)

---

## 📋 Prerequisites

Before running the notebook, ensure you have the following accounts and keys:

* [ ] **Twilio Account:** Account SID, Auth Token, and a purchased phone number.
* [ ] **AssemblyAI Account:** API Key for transcription.
* [ ] **Google Cloud Platform:** Service Account JSON credentials with **Google Sheets** & **Drive API** enabled.
* [ ] **Hugging Face:** Access to `deepseek-ai/deepseek-llm-7b-base`.

---

## 📦 Installation

1.  **Clone this repository:**
    ```bash
    git clone [https://github.com/yourusername/DeepSeek-Banking-Recovery-Agent.git](https://github.com/yourusername/DeepSeek-Banking-Recovery-Agent.git)
    cd DeepSeek-Banking-Recovery-Agent
    ```

2.  **Open the Notebook:**
    Open `DeepSeek_Banking_Bot.ipynb` in **Google Colab** (recommended) or a local Jupyter environment with GPU support.

3.  **Install dependencies:**
    (These are included in the notebook's first cell)
    ```python
    pip install unsloth transformers datasets trl torch accelerate
    pip install twilio assemblyai gspread oauth2client
    ```

---

## 🔧 Configuration

In the **"Automation"** section of the notebook, replace the placeholder variables with your actual credentials:

```python
TWILIO_SID = "your_twilio_sid"
TWILIO_AUTH_TOKEN = "your_twilio_token"
ASSEMBLYAI_KEY = "your_assemblyai_key"
GOOGLE_SHEET_URL = "your_google_sheet_url"
```
## 🏃‍♂️ Usage Guide

The notebook is divided into three logical parts. **You must run them in order:**

### 1. Model Training
Run the training cells to download **DeepSeek-7b** and fine-tune it on the provided dataset. The dataset includes examples such as:

* **User:** "I can't pay until my salary comes." → **Intent:** `Financial Hardship`
* **User:** "I'll clear it by Tuesday." → **Intent:** `Promise to Pay`

### 2. Local Inference
Test the model locally by typing text inputs to see if the model correctly identifies the intent before enabling voice calls.

### 3. Voice Automation Loop
1.  Upload your `credentials.json` (Google Service Account) to the Colab runtime.
2.  Ensure your Google Sheet has the following columns: `Name`, `Date`, `Phone`, `Status`.
3.  Run the automation loop. The script will iterate through rows, make calls, and fill the **Status** column automatically.

---

## ⚠️ Disclaimer

> **Important:** This project is for educational and demonstration purposes only. Automated calling systems must comply with local regulations (such as **TCPA** in the US or **TRAI** regulations in India). Ensure you have explicit consent before calling real phone numbers.

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## 📄 License

[MIT](https://choosealicense.com/licenses/mit/)
