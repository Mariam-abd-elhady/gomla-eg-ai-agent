
# Gomla.eg AI Customer Support Agent

An AI-powered customer support workflow built with **n8n**, **Google Gemini**, and **Qdrant** for a fictional Cairo-based e-commerce store, Gomla.eg.

The system uses **RAG (Retrieval-Augmented Generation)** to answer customer questions from a dedicated FAQ knowledge base, then sends the generated answer for **human approval** before accepting or rejecting it.

---

## Project Overview

The workflow allows customers to submit questions about Gomla.eg, such as:

- Shipping costs
- Delivery times
- Payment methods
- Returns
- Customer support
- Order tracking

The AI Agent retrieves relevant information from the Gomla.eg FAQ stored in Qdrant and generates a concise answer.

Before the answer is finalized, a human reviewer receives an email with **Approve** and **Reject** links.

---

## Architecture

### 1. FAQ Ingestion Workflow

```text
Manual Trigger
      ↓
Edit Fields
      ↓
Default Data Loader
      ↓
Recursive Character Text Splitter
      ↓
Gemini Embeddings
      ↓
Qdrant Vector Store
````

The FAQ is split into chunks, converted into embeddings, and stored in a Qdrant collection named `gomla_faq`.

The collection contains **9 vector points**.

### 2. Main AI Agent Workflow

```text
Webhook
   ↓
AI Agent
   ↓
Gmail Approval Request
   ↓
Wait for Human Response
   ↓
If
 ↙   ↘
Approve  Reject
   ↓       ↓
Response  Fallback Response
```

The AI Agent uses Gemini and the Qdrant Vector Store as a retrieval tool.

---

## Features

* RAG-based FAQ retrieval
* Google Gemini AI Agent
* Qdrant vector database
* Semantic search using embeddings
* Webhook-based customer questions
* Human-in-the-loop approval
* Approve / Reject workflow
* Email approval requests
* No paid APIs required for the implementation

---

## Setup

### Requirements

* n8n
* Google Gemini API credentials
* Qdrant account
* Gmail credentials

### Import the workflows

Import the provided:

* `ingestion.json`
* `agent_main.json`

Then configure your own credentials for:

* Gemini
* Qdrant
* Gmail

> API keys and credentials are not included in this repository.

---

## Testing

The workflow was tested using a POST request containing:

```json
{
  "question": "How much does shipping cost?"
}
```

The AI Agent retrieved the relevant FAQ information and generated an answer.

The human approval flow was tested successfully for both:

* **Approve** → returns the AI-generated response
* **Reject** → returns a polite fallback response

The execution trace also confirms the use of the Qdrant retrieval tool.

---

## Screenshots

The `screenshots/` folder contains screenshots showing:

* Credentials
* FAQ ingestion workflow
* Qdrant vector database
* AI Agent configuration
* Vector Store tool
* Complete main workflow
* Approval email
* Approve and Reject tests
* Execution history
* Vector Store tool trace

---

## Project Files

```text
├── README.md
├── faq.md
├── ingestion.json
├── agent_main.json
└── screenshots/
```

---

## Deliverables

* `faq.md` — Gomla.eg FAQ knowledge base
* `ingestion.json` — FAQ ingestion workflow
* `agent_main.json` — Main AI Agent and human approval workflow
* `screenshots/` — Project implementation and testing evidence
* `README.md` — Project documentation


