# LangChain Module Files

Jupyter notebooks from the **LangChain** module of the Udemy "AI Engineer" course. They walk through the OpenAI API basics and then build up LangChain fundamentals — Model I/O, Output Parsers, LCEL (LangChain Expression Language), and a full Retrieval-Augmented Generation (RAG) pipeline.

Several notebooks have a companion **`- Updated`** version. The originals were written against LangChain 0.x/0.3.x; the `- Updated` notebooks rewrite the same lesson for **LangChain 1.2.x**, where legacy functionality (old chains, some output parsers, community re-exports) moved out of `langchain` and into the separate `langchain-classic` package, and `Chroma` moved from `langchain_community.vectorstores` into the standalone `langchain-chroma` package. When both versions of a notebook exist, prefer the `- Updated` one.

## Folder structure

Notebooks are grouped into folders by module/category, mirroring the course structure:

```
The OpenAI API.ipynb   (env setup + OpenAI API basics, at repo root)
05 - Model IO/
07 - Output Parsers/
08 - LCEL/
09 - RAG/            (also contains the sample source documents used by the loaders)
```

## Contents

### `The OpenAI API.ipynb` (repo root)
The original course split environment setup (module 03) and OpenAI API basics (module 04) across four separate notebooks with a lot of repeated boilerplate (the same `%dotenv` + `openai.api_key` + `client` setup at the top of each). They've been consolidated into a single, code-focused notebook: 1. Setting the API key as an environment variable (`.env` + `%dotenv`, plus the `load_dotenv()` alternative) → 2. First chat completion call (no LangChain) → 3. A sarcastic chatbot with system/user messages → 4. `max_tokens`, `temperature`, `seed`, and `stream`.

### `05 - Model IO/`
The original course split this module across seven notebooks (three of which had a companion `- Updated` version), each repeating the same `pip show langchain` / `%dotenv` / `ChatOpenAI(...)` boilerplate. They've been consolidated into a single notebook that defines one `chat` model and one few-shot `chat_template` and reuses each throughout:

| Notebook | Topic |
|---|---|
| `05 Model IO.ipynb` | 1. `ChatOpenAI` — creating and invoking a chat model → 2. `SystemMessage` / `HumanMessage` / `AIMessage` (incl. multi-turn history) → 3. `PromptTemplate` → 4. `ChatPromptTemplate` → 5. Few-shot chat prompt templates → 6. Chains: legacy `LLMChain` vs. the modern LCEL `prompt \| model` pipe |

### `07 - Output Parsers/`
| Notebook | Topic |
|---|---|
| `07 Output Parsers 01.ipynb` | `StrOutputParser` |
| `07 Output Parsers 02.ipynb` | `CommaSeparatedListOutputParser` |
| `07 Output Parsers 03.ipynb` / `- Updated` | `DatetimeOutputParser` (moved to `langchain_classic.output_parsers` in the updated version) |

### `08 - LCEL/` (LangChain Expression Language)
| Notebook | Topic |
|---|---|
| `08 LCEL 01.ipynb` | Piping a prompt, model, and output parser together |
| `08 LCEL 02.ipynb` | Batching |
| `08 LCEL 03.ipynb` | Streaming |
| `08 LCEL 04.ipynb` | The `Runnable` and `RunnableSequence` classes |
| `08 LCEL 05.ipynb` | Piping chains with `RunnablePassthrough` |
| `08 LCEL 06.ipynb` | Graphing (visualizing) runnables |
| `08 LCEL 07.ipynb` | `RunnableParallel` |
| `08 LCEL 08.ipynb` | Piping a `RunnableParallel` with other runnables |
| `08 LCEL 09.ipynb` | `RunnableLambda` |
| `08 LCEL 10.ipynb` | The `@chain` decorator |

### `09 - RAG/` (Retrieval-Augmented Generation)
Follows the classic **Indexing → Retrieval → Generation** RAG pipeline:

| Notebook | Topic |
|---|---|
| `09 RAG 06.ipynb` / `- Updated` | **Indexing** — document loading with `PyPDFLoader` |
| `09 RAG 07.ipynb` | **Indexing** — document loading with `Docx2txtLoader` |
| `09 RAG 09.ipynb` | **Indexing** — document splitting with `CharacterTextSplitter` |
| `09 RAG 10.ipynb` | **Indexing** — document splitting with `MarkdownHeaderTextSplitter` |
| `09 RAG 11.ipynb` | **Indexing** — text embedding with OpenAI embeddings |
| `09 RAG 12.ipynb` / `- Updated` | **Indexing** — creating a Chroma vector store |
| `09 RAG 13.ipynb` / `- Updated` | **Indexing** — inspecting and managing documents in a vector store |
| `09 RAG 14.ipynb` / `- Updated` | **Retrieval** — similarity search |
| `09 RAG 15.ipynb` / `- Updated` | **Retrieval** — maximal marginal relevance (MMR) search |
| `09 RAG 16.ipynb` / `- Updated` | **Retrieval** — vector-store-backed retriever |
| `09 RAG 17.ipynb` / `- Updated` | **Generation** — stuffing retrieved documents into the prompt |
| `09 RAG 18.ipynb` / `- Updated` | **Generation** — generating the final response |

Also contains the reference/source documents used by the loaders above:

| File | Description |
|---|---|
| `Introduction_to_Data_and_Data_Science.pdf` / `.docx` | Sample source document used as input for the RAG document-loading notebooks (`09 RAG 06`–`09 RAG 18`) |
| `Introduction_to_Data_and_Data_Science_2.docx` | Alternate/updated version of the sample source document |

These sit alongside the notebooks in the same folder because the loaders reference them with relative filenames (e.g. `PyPDFLoader("Introduction_to_Data_and_Data_Science.pdf")`), so the notebook's working directory must match.

## Setup

### 1. Create and activate an environment
This folder already contains a conda environment at `venv/`. Activate it, or create your own:

```bash
conda activate "./venv"
# or, from scratch:
conda create -p ./venv python=3.11
conda activate "./venv"
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Set your OpenAI API key
Create a `.env` file in the **repo root** (see section 1 of `The OpenAI API.ipynb` for the full walkthrough). `python-dotenv` searches upward from a notebook's working directory, so a root-level `.env` is found regardless of which subfolder a notebook lives in:

```
OPENAI_API_KEY="sk-..."
```

The notebooks load it via:

```python
%load_ext dotenv
%dotenv
```

### 4. Register the Jupyter kernel and run
If Jupyter can't find your environment as a kernel:

```bash
python -m ipykernel install --user --name langchain_env --display-name "langchain_env"
```

Then open any notebook and select the `langchain_env` kernel, or run:

```bash
jupyter notebook
```

## Notes

- Prefer the `- Updated` notebooks — they reflect LangChain 1.2.x's current package layout (`langchain-classic`, `langchain-chroma`, etc.). The non-updated notebooks are kept for reference but use import paths that no longer exist in current LangChain versions.
- The RAG notebooks write a persisted Chroma vector store to disk (ignored via `.gitignore`); rerun the indexing notebooks (`09 RAG 06`–`13`) before the retrieval/generation ones if you clear that store.
- Never commit your `.env` file or hardcode your API key — see section 1 of `The OpenAI API.ipynb` for why.
