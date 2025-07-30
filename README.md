# Lyra Sentiment Classifier (n8n + GPT-4.1 nano)

This project demonstrates a fast and modular sentiment analysis workflow using **n8n**, integrated with **GPT-4.1 nano** via OpenAI Assistant, and routing results to separate **Google Sheets** based on sentiment category.

## 🌐 Overview

- 🔁 Loops over multiple short texts from a Google Sheet
- 🧠 Sends each text to a custom GPT assistant for sentiment analysis
- ⚖️ Parses the output JSON (`{ "sentiment": "Positive" }`)
- 🧭 Routes to one of three categories: **Positive**, **Negative**, **Neutral**
- ⏱️ Includes a `Wait` node (500 ms) to regulate API call frequency
- 📄 Appends results to the corresponding sentiment-specific Google Sheet

## 🛠 Workflow Structure

```
/Sentiment_Analysis/
├── /screenshot/
│   └── Workflow.png
├── /code/
│   ├── JS Parsing.txt
│   └── Sentiment_Analysis_workflow.json
└── README.md
```

## 🔁 Parsing Logic (JS node)

```javascript
const parsed = JSON.parse($json.output);
return { sentiment: parsed.sentiment };
```

## 🧠 Prompt used in GPT Assistant

```txt
You are a sentiment analysis assistant. Categorize the sentiment of the input text as one of: "Positive", "Neutral", or "Negative".

Return only a JSON object with the following structure:

{ "sentiment": "Positive" }

Do not add any commentary, explanation, or text outside the JSON object.
```

## 🧪 Usage Notes

- Works best for up to 20–50 texts per run.
- A `Wait 500 ms` block is used after each LLM call to prevent throttling.
- Each sentiment type is logged in a separate Google Sheet.

## 📤 Importing the Workflow

To import the workflow into your own instance of n8n:

1. Go to **n8n.io** or your self-hosted instance.
2. Import the JSON file from `code/Sentiment_Analysis_workflow.json`.
3. Configure your **Google Sheets** and **OpenAI credentials**.
4. Add your GPT Assistant with the provided prompt.

---

© 2025 – Project by Jérôme (Lyra)