---
title: Chat with Krishna using GitaGPT AI
slug: chat-with-krishna-using-gitagpt-ai
pubDate: 2025-04-20
description: Chat with Lord Krishna using GitaGPT—an AI-powered tool that answers your questions with wisdom from the Bhagavad Gita.
author: Ashish Khare
hasAudio: false
---

![banner](./assets/chat-with-krishna-using-gitagpt-ai/banner.webp)

Ever wondered what it would be like to get answers from Lord Krishna himself?  
Meet **GitaGPT** — your AI companion that brings the wisdom of the _Bhagavad Gita_ right into your hands. Whether you're lost in thought, curious about life, or just looking for some timeless advice, GitaGPT has got your back — calm, collected, and always Krishna-like.

This isn’t your regular chatbot. It’s built to help you explore questions through the lens of spiritual wisdom, in the same way Krishna guided Arjuna through the chaos of Kurukshetra.

---

## 🌟 What Makes GitaGPT Special?

### 🔁 Retrieval-Augmented Generation (RAG) with Gemini

We’re not generating fluff. GitaGPT uses **Google Gemini**’s language model in combo with a **vector store** to pull out actual, relevant verses from the Bhagavad Gita before crafting a response. So every answer is both smart and rooted in scripture.

### 📚 Verse-backed Responses

Every response isn’t just “Krishna said…” — it includes **actual verse references** from the Gita, like _Verse 2.47_ or _Verse 11.38_. You get real context, not just paraphrasing.

### 🧠 Powered by Gemini LLM

Thanks to **Gemini 2.0 Flash**, the chatbot feels smooth, responsive, and can hold a tone that’s friendly yet wise — like Krishna gently nudging Arjuna toward clarity.

### 💾 ChromaDB Integration

All verses from the Gita are stored in a vector database using **ChromaDB**, allowing super-fast and accurate search. This ensures the chatbot pulls out passages that actually match what you're asking.

### 🧩 Modular Prompting

The prompts are structured beautifully:

- **Prompt tone**: Like a teacher explaining softly to a student.
- **Question**: From you.
- **Passages**: Fetched based on similarity to your question.
- **Output**: A well-formed JSON with a summary, keywords, and verse references.

### 🖼️ Beautiful Markdown Output

Answers are formatted in **clean Markdown**, so whether you're reading on Kaggle or your own notebook, everything looks neat and digestible.

---

## 📖 How GitaGPT Works (Under the Hood)

### 1. **Document Loading**

We start by loading the full text of the Bhagavad Gita using `TextLoader`. Then, it’s split into small overlapping chunks using `RecursiveCharacterTextSplitter` so we don’t lose context.

### 2. **Embedding with Gemini**

Using a custom `GeminiEmbeddingFunction`, every chunk of text is turned into a vector embedding — which is like giving the model a memory of what each passage means.

### 3. **Storing in ChromaDB**

These embeddings are stored in a ChromaDB collection. Later, when a user asks something, we query this vector store to fetch the most relevant chunks.

### 4. **Generating a Response**

The retrieved verses + your question are bundled into a smart prompt, and sent to Gemini’s `generate_content()` function. It replies with a structured answer in a JSON format — which we display cleanly.

---

## 🚀 Why You’ll Love It

- It’s **spiritually aware**, not just AI-smart.
- You’re always backed by **authentic references**.
- It’s **fun, calming, and surprisingly insightful**.
- It's like talking to Krishna — **seriously**.

---

## 🌈 Coming Soon

- 🔊 Voice responses with TTS
- 🌐 Web app interface
- 📱 Mobile app for daily Gita wisdom
- 🔄 More dynamic prompt customization

---

## Ready to Ask?

GitaGPT is more than a tool — it's a spiritual companion in your coding journey. Ask about purpose, duty, peace, or even the meaning of life.

Just like Arjuna, you might discover answers you never expected.

**Try it. Reflect. Repeat. 🧘**
