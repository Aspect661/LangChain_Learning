# LangChain Module Files

Jupyter notebooks from the **LangChain** module of the Udemy "AI Engineer" course. They walk through the OpenAI API basics and then build up LangChain fundamentals — Model I/O, Output Parsers, LCEL (LangChain Expression Language), and a full Retrieval-Augmented Generation (RAG) pipeline.

Several notebooks have a companion **`- Updated`** version. The originals were written against LangChain 0.x/0.3.x; the `- Updated` notebooks rewrite the same lesson for **LangChain 1.2.x**, where legacy functionality (old chains, some output parsers, community re-exports) moved out of `langchain` and into the separate `langchain-classic` package, and `Chroma` moved from `langchain_community.vectorstores` into the standalone `langchain-chroma` package. When both versions of a notebook exist, prefer the `- Updated` one.

## Folder structure

Notebooks are grouped into folders by module/category, mirroring the course structure:

```
03 - Setting Up the Env/
04 - The OpenAI API/
05 - Model IO/
07 - Output Parsers/
08 - LCEL/
09 - RAG/            (also contains the sample source documents used by the loaders)
```

## Contents

### `03 - Setting Up the Env/`
| Notebook | Topic |
|---|---|
| `03 Setting Up the Env 03.ipynb` | Storing your OpenAI API key in a `.env` file and loading it as an environment variable with the `dotenv` IPython extension |

### `04 - The OpenAI API/`
| Notebook | Topic |
|---|---|
| `04 The OpenAI API 01.ipynb` | First steps calling the OpenAI API directly (no LangChain) |
| `04 The OpenAI API 03.ipynb` | Creating a sarcastic chatbot |
| `04 The OpenAI API 04.ipynb` | Temperature, max tokens, and streaming responses |

### `05 - Model IO/`
| Notebook | Topic |
|---|---|
| `05 Model IO 02.ipynb` / `- Updated` | `ChatOpenAI` — instantiating and invoking a chat model |
| `05 Model IO 03.ipynb` / `- Updated` | System and human messages |
| `05 Model IO 04.ipynb` / `- Updated` | AI messages (model responses) |
| `05 Model IO 05.ipynb` | Prompt templates and prompt values |
| `05 Model IO 06.ipynb` | Chat prompt templates and chat prompt values |
| `05 Model IO 07.ipynb` | Few-shot chat message prompt templates |
| `05 Model IO 08.ipynb` | `LLMChain` (legacy chain API) |

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
Create a `.env` file in the **repo root** (see `03 - Setting Up the Env/03 Setting Up the Env 03.ipynb` for the full walkthrough). `python-dotenv` searches upward from a notebook's working directory, so a root-level `.env` is found regardless of which subfolder a notebook lives in:

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
- Never commit your `.env` file or hardcode your API key — see `03 - Setting Up the Env/03 Setting Up the Env 03.ipynb` for why.
