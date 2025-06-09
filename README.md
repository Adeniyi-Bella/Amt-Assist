# AmtAssist: a digital assistant for summarizing government documents.

Final project for the Building AI course

## Summary

AmtAssist is a smart document scanner powered by OCR and Natural Language Processing (NLP) that helps users, especially immigrants and expats in Germany, understand official government letters written in German. Can also be extended to other languages.
The system translates dense bureaucratic language into the user's native language, extracts deadlines, and summarizes required actions in simple terms.

## Background

### The Problem:
Navigating German bureaucracy is notoriously difficult—even for native speakers. Letters from the Ausländerbehörde, Jobcenter, Finanzamt, or Krankenkasse are often:

* Long, complex, and written in formal/legal German,
* Filled with deadlines, technical terms, and implicit instructions,
* Difficult for immigrants or non-native speakers to interpret accurately.

### How common is this?:

* Every immigrant or refugee or foreigner in Germany receives regular government correspondence.
* Germany has millions of foreign residents, many of whom deal with this confusion regularly.
* Even native Germans often find it difficult understanding official letters.

### Personal Motivation:
Having experienced this firsthand as an immigratant, it's clear that a tool to decode, translate, and clarify such documents could massively reduce stress, miscommunication.

## Data sources and AI methods

### Data Sources:
* Scanned letters or PDFs from users (images or text),
* Publicly available samples of bureaucratic letters (e.g., from integration guides or anonymized examples),

### AI Techniques:
1. OCR (Optical Character Recognition)
* Libraries: [Tesseract OCR], [EasyOCR], [Google Vision API]
* To extract raw text from scanned or photographed documents.

2. NLP for Key Information Extraction
* Deadline detection via date entity recognition (e.g., spaCy's DATE entity),
* Action detection via intent extraction and keyword patterns (e.g., "Sie müssen", "Bitte reichen Sie ein...").

3. Summarization & Translation
* Text summarization using transformer models like BART, T5, or GPT-4,
* Translation via MarianMT, mBART, or DeepL API.

4. Multilingual Support
* Allow user to select their native language (e.g., English, Arabic, Ukrainian),
* Translate summary and action list accordingly.

## How is it used?

### Users: 
* Primary: Immigrants, expats, refugees, and non-German speakers living in Germany,
* Secondary: Germans with bureaucratic anxiety, social workers, integration officers, legal aid volunteers.

### Usage Context:
A mobile app or web app where users:
* Upload or scan a document,
* Choose their native language,

* Receive:
✅ Plain-language summary of the letter
✅ Deadlines highlighted
✅ Checklist of required actions
✅ Translated version in their language

This would empower users to take appropriate actions without needing a translator or lawyer for every letter.

## Challenges
* Privacy and data security: Users may upload sensitive personal data—encryption and on-device processing (where possible) are essential.
* Ambiguity in language: Some government letters are vague or rely on context; misinterpretation is still possible.
* Translation accuracy: Automatically translating legal German may lose nuances, especially for languages with fewer resources.
* Handwritten documents: OCR is less reliable on handwriting or poor scans.

## 🏗️ System Architecture

The platform allows users to upload scanned German letters (e.g. from government offices), and uses OCR + NLP + AI to extract key information and provide natural-language summaries in the user's preferred language.

### ✨ High-Level Components

```plaintext
[ User (Web) ]
     |
     |  Upload scanned document
     v
[ Next.js Frontend (with API Routes) ]
     |
     |  → Handles authentication (Azure AD B2C)
     |  → Uploads documents to Azure Blob Storage
     |  → Forwards file reference to backend
     v
[ Python Backend Service ]
     |
     |  → Runs OCR (e.g. Tesseract or PaddleOCR)
     |  → Uses NLP to extract deadlines, required actions
     |  → Calls Azure OpenAI for summary generation
     v
[ Azure Blob Storage ]
     |
     |  Stores: original documents, extracted text, metadata, and summaries
     v
[ User Dashboard ]
     |
     |  Displays:
     |    - Summary of the letter
     |    - Detected deadlines
     |    - Required actions (translated)


## What next?
* Integration with appointment booking systems, e.g., booking an Anmeldung slot directly from the app,
* Chatbot follow-up assistant: Ask questions like “What happens if I miss the deadline?”
* Voice explanations: Especially for people with low literacy,

## Acknowledgments
* OCR: Tesseract OCR (open-source)
* Chat GTP.
* Inspiration: Personal experience.
