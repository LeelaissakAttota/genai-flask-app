# ⚡ GenAI Flask App — Multi-Model AI Customer Assistant

![Language](https://img.shields.io/badge/Language-Python%203.11-3776AB?style=flat-square&logo=python&logoColor=white)
![Framework](https://img.shields.io/badge/Framework-Flask-000000?style=flat-square)
![LLM](https://img.shields.io/badge/LLM-Llama%203.2%20%7C%20Granite%203.3%20%7C%20Mistral%20Small-052FAD?style=flat-square&logo=ibm&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-LCEL%20Chains-FF6B35?style=flat-square)
![Output](https://img.shields.io/badge/Output-Structured%20JSON-2E7D32?style=flat-square)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square)

---

## 📌 Project Overview

A production-style **Flask web application** that routes customer 
queries across **3 IBM Watsonx LLMs** — Llama 3.2, Granite 3.3, 
and Mistral Small — and returns structured JSON responses with 
sentiment scores using LangChain LCEL and Pydantic output parsing.

Select your model, submit a customer message, and instantly get a 
structured AI response with **summary**, **sentiment score (0–100)**, 
and a **suggested reply** — all timed for performance comparison.

**Domain:** GenAI Web App — Customer Service AI  
**LLMs:** Llama 3.2 11B Vision + IBM Granite 3.3 8B + Mistral Small 3.1 24B  
**Platform:** IBM Watsonx.ai  

---

## 📂 Project Structure

```
genai-flask-app/
│
├── app.py          # Flask routes — /generate POST endpoint
├── model.py        # 3 LLM chains + Pydantic JSON parser
├── config.py       # Model IDs + Watsonx credentials
├── capital.py      # Standalone Llama 4 Maverick test script
├── static/
│   └── script.js   # Frontend AJAX calls + response rendering
└── templates/
    └── index.html  # Chat UI with model selector
```

---

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| Backend | Flask |
| LLM 1 | meta-llama/llama-3-2-11b-vision-instruct |
| LLM 2 | ibm/granite-3-3-8b-instruct |
| LLM 3 | mistralai/mistral-small-3-1-24b-instruct-2503 |
| Platform | IBM Watsonx.ai |
| LangChain | ChatWatsonx + LCEL + PromptTemplate |
| Output Parser | JsonOutputParser (Pydantic) |
| Frontend | HTML + JS (AJAX) |

---

## 🤖 3 LLM Chains with Model-Specific Prompt Templates

Each model uses a **dedicated prompt template** matching its native format:

```python
# Llama — chat tokens
llama_template = "<|begin_of_text|><|start_header_id|>system<|end_header_id|>
{system_prompt}\n{format_prompt}...<|start_header_id|>assistant<|end_header_id|>"

# Granite — simple system/human/AI format
granite_template = "System: {system_prompt}\n{format_prompt}\nHuman: {user_prompt}\nAI:"

# Mistral — [INST] instruction format
mistral_template = "<s>[INST]{system_prompt}\n{format_prompt}\n{user_prompt}[/INST]"
```

---

## 📊 Structured JSON Output (Pydantic)

```python
class AIResponse(BaseModel):
    summary: str   = Field(description="Summary of the user's message")
    sentiment: int = Field(description="Sentiment score 0 (negative) to 100 (positive)")
    response: str  = Field(description="Suggested response to the user")
```

**Every model returns:**
```json
{
  "summary": "Customer asking about order status",
  "sentiment": 45,
  "response": "I'd be happy to help track your order...",
  "duration": 1.23
}
```

---

## 🚀 LCEL Chain per Model

```python
def get_ai_response(model, template, system_prompt, user_prompt):
    chain = template | model | json_parser
    return chain.invoke({
        'system_prompt': system_prompt,
        'user_prompt': user_prompt,
        'format_prompt': json_parser.get_format_instructions()
    })
```

---

## ⚙️ Flask API

```
POST /generate
Body: { "message": "Where is my order?", "model": "llama" }
Response: { "summary": "...", "sentiment": 45, "response": "...", "duration": 1.2 }
```

---

## 🎓 Skills Demonstrated

- Flask REST API with JSON request/response
- 3 IBM Watsonx LLMs in one app — Llama + Granite + Mistral
- Model-specific prompt templates (Llama tokens, Granite format, Mistral INST)
- LangChain LCEL chains — `template | model | json_parser`
- Pydantic `JsonOutputParser` for structured AI output
- Sentiment scoring (0–100) via LLM
- Response time measurement per model
- Frontend AJAX + dynamic model selection
- Customer service AI assistant use case

---

## 📜 Certifications

| Certification | Issuer | Platform |
|---|---|---|
| IBM Data Science Professional Certificate | IBM | Coursera |
| IBM Generative AI Professional Certificate | IBM | Coursera |
| IBM Agentic AI with RAG Certificate | IBM | Coursera |
| IBM RAG and Agentic AI Professional Certificate | IBM | Coursera |

---

## 🤝 Connect with Me

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Leela%20A-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/leela-a)
[![Gmail](https://img.shields.io/badge/Gmail-attotaleelaissak@gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:attotaleelaissak@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-Leelaissakattaota-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/Leelaissakattaota)
