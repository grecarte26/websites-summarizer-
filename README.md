# websites-summarizer-
# 🧠 Website Digest Summarizer

**Author:** Jerson  
**Project Type:** Python Script  
**Model Used:** LLaMA 3 (via Ollama)

---

## 📌 Overview

**Website Digest Summarizer** is a Python-based tool that:

- Scrapes and extracts clean text content from any webpage
- Removes unnecessary HTML elements like scripts, styles, and images
- Uses a local LLM (Large Language Model) via **Ollama** to summarize the content into a short, readable paragraph

This project is ideal for researchers, students, or anyone looking to quickly digest the key points of a website without reading the entire page.

---

## 🚀 Features

- Web scraping with `requests` and `BeautifulSoup`
- Summarization powered by `llama3` or any other supported model on [Ollama](https://ollama.com)
- Clear, modular code using a `Website` class
- Works with any public webpage URL

---

## 🔧 Requirements

Make sure you have these installed in your Python environment:

```bash
pip install requests beautifulsoup4 ollama
