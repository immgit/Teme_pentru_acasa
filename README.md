# Teme pentru acasă

Acest repository conține temele pentru acasă realizate în cadrul unui curs de Inteligență Artificială / Machine Learning. Proiectul central este un **RAG Assistant** (Retrieval-Augmented Generation) — un chatbot web care răspunde la întrebări pe baza documentelor extrase de pe internet, folosind un model de limbaj (LLM).

## Structura repository-ului

| Director / Fișier | Descriere |
|---|---|
| `app/main.py` | Aplicația web **FastAPI** care expune endpoint-urile `/` și `/chat/` pentru interacțiunea cu RAG Assistant-ul |
| `src/tema_2_services/service.py` | Clasa `RAGAssistant` — nucleul aplicației: încarcă documente web, le împarte în chunk-uri, creează embeddings cu **Universal Sentence Encoder**, indexează cu **FAISS** și generează răspunsuri prin LLM (Groq API) |
| `tema_3_evaluation/` | Evaluarea calității răspunsurilor folosind **deepeval** și abordarea *LLM-as-a-Judge* (cu metrici GEval) |
| `tema_3_tests/test_main.py` | Teste pentru endpoint-urile aplicației |
| `_non-code/tema_1_idee_afacere/` | **Tema 1** — Generare de idei de afaceri folosind tehnici de prompting (zero-shot, few-shot, chain-of-thought, ReAct) |
| `_non-code/tema_4_videoclipuri/` | **Tema 4** — Prompturi pentru generare de videoclipuri |
| `requirements.txt` | Dependențele Python ale proiectului |
| `.env.sample` | Exemplu de fișier de configurare cu variabilele de mediu necesare |

## Tehnologii utilizate

- **FastAPI** + **Uvicorn** — server web asincron
- **LangChain** (`WebBaseLoader`, `RecursiveCharacterTextSplitter`) — încărcare și procesare documente
- **TensorFlow** + **TensorFlow Hub** — Universal Sentence Encoder pentru embeddings
- **FAISS** — indexare și căutare vectorială rapidă
- **OpenAI SDK** (cu Groq API) — generare răspunsuri LLM
- **deepeval** — evaluare calitate răspunsuri (LLM-as-a-Judge)
- **Groq** — provider LLM alternativ pentru evaluare
- **pytest** — framework de testare

## Configurare și rulare

1. **Clonează repository-ul** și creează un mediu virtual:
   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/Mac
   # sau: venv\Scripts\activate  # Windows
   ```

2. **Instalează dependențele**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Configurează variabilele de mediu** — copiază `.env.sample` în `.env` și completează valorile:
   ```bash
   cp .env.sample .env
   ```
   Variabile necesare:
   - `GROQ_API_KEY` — cheia API pentru Groq
   - `WEB_URLS` — URL-urile sursă pentru documente (separate prin `;`)

4. **Pornește serverul**:
   ```bash
   uvicorn app.main:app --host 0.0.0.0 --port 8000
   ```

5. **Testează**:
   ```bash
   pytest tema_3_tests/
   ```

6. **Evaluare** (necesită serverul pornit):
   ```bash
   python -m tema_3_evaluation.evaluate
   ```
