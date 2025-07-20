# Text-to-Structured JSON Extractor using Gemma 2 (9B) + Gradio

This project uses Google's **Gemma-2 9B Instruction-Tuned** model to convert **unstructured text** into **structured JSON output** based on a defined `schema.json`. It includes an interactive Gradio interface for rapid testing.

---

## Model

* **Model Used**: [`google/gemma-2-9b-it`](https://huggingface.co/google/gemma-2-9b-it)
* **Framework**: Hugging Face Transformers
* **Device Support**: Automatically uses available GPUs with `device_map="auto"`

---

## Project Structure

```bash
.
├── schema.json           # JSON Schema for structuring output
├── text_to_json.ipynb    # Main notebook
```

> The model uses `schema.json` to format any given unstructured input into a strictly valid JSON structure.

---

##  Features

* Multi-GPU support (auto-distribution for large models like Gemma 9B)
* Gradio interface for real-time JSON generation
* Schema-based control over output format
* Fallback error handling for JSON decode failures

---

##  How it Works

1. Load `schema.json`
2. Prepare a prompt that includes:

   * The unstructured input
   * The schema
3. Send the prompt to Gemma-2 9B
4. Postprocess the model output and extract valid JSON
5. Serve it via Gradio

---

##  Running Locally (Kaggle or Colab)

> This project is designed to be run in a **Jupyter Notebook environment** like **Kaggle** or **Google Colab** with GPU support.

**Steps:**

1. Upload `schema.json` to your notebook environment
2. Ensure you have access to the HuggingFace Hub and the Gemma 2 9B model
3. Run all cells in `text_to_json.ipynb`
4. Use the Gradio UI to input unstructured text and view the structured output

---

## Environment Variables

To keep your HuggingFace access token safe:

```python
import os
os.environ["HF_TOKEN"] = "your_hf_token_here"
```

Or use `.env` (only for Python scripts, not notebooks)

```env
HF_TOKEN=your_token
```

---

## Dependencies

```bash
transformers
accelerate
torch
gradio
```

Install via pip:

```bash
pip install transformers accelerate torch gradio
```

---

## Example Input

```text
Create an action that builds MkDocs documentation and deploys it to GitHub Pages...
```

## Example Output (Structured JSON)

```json
{
  "action_name": "MkDocs Publisher",
  "purpose": "A simple action to build an MkDocs site and push it to the gh-pages branch.",
  "author": "DevRel Team",
  ...
}
```

---

## Model Behavior Notes

* **Gemma 2 9B** generates reliable structured outputs if prompted well
* Schema injection helps the model maintain format fidelity
* Error handling in the notebook helps catch and debug malformed responses

---
