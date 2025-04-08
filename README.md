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
#### this is the final code
# Project: Website Digest Summarizer
# Author: Jerson
# Description:
# This script scrapes the content from a webpage, removes irrelevant elements,
# and summarizes the text using a local LLM model via Ollama.

# -------- IMPORTS --------
import requests
from bs4 import BeautifulSoup
import ollama

# -------- CLASS DEFINITION --------
class Website:
    """
    A utility class to represent a Website that we have scraped
    """

    def __init__(self, url):
        """
        Create this Website object from the given URL using BeautifulSoup
        """
        self.url = url
        response = requests.get(url)
        soup = BeautifulSoup(response.content, 'html.parser')
        self.title = soup.title.string if soup.title else "No title found"

        # Remove scripts, styles, images, and form inputs
        for irrelevant in soup.body(["script", "style", "img", "input"]):
            irrelevant.decompose()

        # Extract visible text
        self.text = soup.get_text(separator="\n", strip=True)

# -------- USAGE EXAMPLE --------

# Replace with any webpage you'd like to summarize
cnn = Website("https://www.cnn.com/")

print("📰 Title:", cnn.title)
print("\n🔍 Preview of Extracted Text:\n")
print(cnn.text[:1000])  # Show a limited preview

# -------- GENERATE SUMMARY USING OLLAMA --------
response = ollama.chat(
    model='llama3',  # Ensure this model is installed via Ollama
    messages=[
        {"role": "system", "content": "Summarize this webpage content in a concise paragraph."},
        {"role": "user", "content": cnn.text}
    ]
)

summary = response['message']['content']
print("\n🧠 Summary:\n")
print(summary)

