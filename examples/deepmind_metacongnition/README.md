# 🧠 DeepMind Metacognition Guardrail: Curing the "Helpfulness Bias"

This folder contains the RCCO implementation and testing environment used for the **Google DeepMind "Measuring Progress Toward AGI"** Kaggle competition.

## The Problem: The Helpfulness Bias
Current frontier models are heavily optimized via RLHF (Reinforcement Learning from Human Feedback) to be "helpful assistants." This creates a dangerous cognitive bias: models are implicitly penalized during training for refusing to answer a prompt.

When faced with a complex prompt where critical variables are missing (making the problem mathematically or logically unsolvable), models will often hallucinate the missing variables just so they can provide a "helpful" calculation. They fail at **Metacognitive Inhibition**—the ability to know when to stop.

## The Solution: The RCCO Guardrail
By wrapping standard prompts in an **Epistemically Rigorous RCCO Framework**, we can override the RLHF "helpful" persona. The RCCO framework explicitly enforces:
1. **System 2 Parameter Validation:** Forcing the model to map all variables before attempting a calculation.
2. **The Zero-Assumption Mandate:** Strictly forbidding the hallucination of ideal states (e.g., a frictionless vacuum).

## 🧪 The Ablation Study (`ablation.py`)
This script proves that the RCCO framework successfully acts as a Metacognitive Scaffold. 

It feeds a frontier model (Gemini 2.5 Flash) physically unsolvable kinematics problems in two states:
1. **Control Group (Standard Prompting):** The model typically succumbs to the Helpfulness Bias and hallucinates an answer.
2. **Treatment Group (RCCO Guardrail):** The model successfully inhibits its response, explicitly refuses the calculation, and identifies the missing physical parameter.

### How to Run the Study
1. Ensure you have the `google-genai` SDK installed:
   ```bash
   pip install google-genai python-dotenv

Export your Gemini API key to your environment (or place it in a .env file at the root of the repository):

GEMINI_API_KEY="your_api_key_here"

Execute the script from the root of the repository:

python examples/deepmind_metacognition/ablation.py