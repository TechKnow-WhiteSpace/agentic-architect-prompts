# 🏛️ The Agentic Architect Prompt Library

[![Status: Active](https://img.shields.io/badge/Status-Active-brightgreen.svg)]()
[![Google AI Studio](https://img.shields.io/badge/Tested_in-Google_AI_Studio-blue.svg)]()
[![Gemini API](https://img.shields.io/badge/Powered_by-Gemini_API-orange.svg)]()

Welcome to the **Agentic Architect Prompt Library**. 

In production software, we don't "chat" with AI; we program it. This repository contains a curated collection of battle-tested System Instructions designed to be used via the Gemini API, Vertex AI SDK, or Google AI Studio.

These prompts are engineered to prevent hallucinations, enforce strict formatting (like JSON or structured Markdown), and keep the model perfectly in character for headless application backends.

---

## 📐 The RCCO Architecture

Every prompt in this library abandons "voodoo prompting" (e.g., "take a deep breath", "I will tip you") in favor of strict systems engineering. 

They all follow the **RCCO Framework**:
* **R**ole: Who the agent is and its level of expertise.
* **C**ontext: The situation and what the user will provide.
* **C**onstraints: The unbreakable rules the agent must follow (what NOT to do).
* **O**utput Format: The exact data structure the frontend/backend expects to receive.

---

## 🚀 How to Use These Prompts

**1. In Google AI Studio (Prototyping)**
Paste the prompt text directly into the **"System Instructions"** panel on the left side of the screen.

**2. In Python (Production via `google-genai`)**
Bind the prompt to the `GenerateContentConfig` object before calling the model:

```python
from google import genai
from google.genai import types

client = genai.Client()

system_prompt = """[PASTE PROMPT FROM THIS LIBRARY HERE]"""

config = types.GenerateContentConfig(
    system_instruction=system_prompt,
    temperature=0.2 # Keep temperature low for structured tasks
)

response = client.models.generate_content(
    model='gemini-2.5-pro',
    contents='[User Input]',
    config=config
)
```

## 🏆 Featured Use Case: Google DeepMind AGI Benchmarking
The RCCO Framework is currently being utilized in the **Google DeepMind "Measuring Progress Toward AGI"** Kaggle competition to solve the critical "Helpfulness Bias" in LLM-as-a-Judge evaluation pipelines.

When standard prompts allow models too much creative freedom, they frequently hallucinate scores, ignore constraints, or output malformed JSON that crashes automated SDKs (like `kaggle-benchmarks`). 

By enforcing strict **System 2 Parameter Validation** and a **Zero-Assumption Mandate**, the RCCO Framework creates *semantically immutable* system instructions. This ensures deterministic, JSON-strict outputs required for enterprise-grade benchmarking.

👉 **[View the DeepMind Metacognition Ablation Study Example](./examples/deepmind_metacognition/)**

## 📚 The Prompt Library Directory

Browse the open-source collection of RCCO prompts. Click on any use-case to view the full system instructions.

* 🧠 **[DeepMind Metacognition Guardrail](./examples/deepmind_metacognition/)**: Cures the "Helpfulness Bias" in LLM Judges (Includes a runnable Python Ablation Study).
* 🛡️ **[The PII Redaction Agent](./examples/pii_redaction_agent/prompt.md)**: A security-first pipeline that sanitizes sensitive user data (names, SSNs, phone numbers) before passing it to downstream systems.
* 📑 **[The RAG Synthesizer](./examples/rag_synthesizer/prompt.md)**: Forces the model to answer queries *strictly* using retrieved context chunks, preventing out-of-bounds hallucinations.
* ⚙️ **[The Strict JSON Extractor](./examples/strict_json_extractor/prompt.md)**: Headless pipeline for converting unstructured text or document images into clean JSON.
* 👁️ **[The UX/UI Video Critic](./examples/ux_ui_critic/prompt.md)**: Multimodal prompt for conducting professional accessibility and design audits from screenshots or video.
* 💻 **[The Code-Reviewing Copilot](./examples/code_review_copilot/prompt.md)**: Staff-level automated GitHub PR reviews that hunt for algorithmic flaws and security vulnerabilities.



📖 About the Series
This library was created as part of the Agentic Architect Series—a technical deep dive into building production-grade AI agents using the Google Cloud stack (Gemini, Vertex AI, Firebase Genkit).

Read Part 4 of the series: Prompt Engineering Lab: Mastering System Instructions.

🤝 Contributing
Have a bulletproof system instruction you use in production? Pull Requests are welcome! Please ensure any submitted prompts follow the RCCO framework.

Created by Ben White. License: MIT.
