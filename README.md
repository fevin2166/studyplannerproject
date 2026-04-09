Local AI Tutor & Study Planner
An interactive, locally-hosted AI tutor built with Streamlit, Llama.cpp, and Reinforcement Learning. The tutor dynamically adjusts its pedagogical strategy (Analogy, Socratic Questioning, Break Suggestions) based on real-time metrics including your typing delay, response length, and estimated fatigue. The project also features a Retrieval-Augmented Generation (RAG) system allowing the tutor to reference uploaded PDFs.
Features
Local LLM Integration: Uses `llama-cpp-python` to run GGUF models completely offline with no external APIs.
Dynamic RL Teaching Strategy: A PPO trained agent (`stable-baselines3`) simulates student states and recommends the best teaching style based on real-time fatigue and engagement tracking.
RAG Knowledge Base: Upload PDFs via the UI and converse about the context seamlessly. Uses `ChromaDB` for vector storage and `PyPDF2` (and `PyMuPDF`) for text extraction.
Teacher's Dashboard: Sidebar interface displaying real-time metrics on fatigue, current teaching style, and system performance.
Prerequisites
Python 3.8+
C/C++ Compiler: Often required by `llama-cpp-python` or `ChromaDB` if wheels (pre-built binaries) are unavailable.
Local GGUF Model:
The app looks for a model named `model.gguf` in the repository root directory. You can download one from Hugging Face (e.g., an instruction-tuned model like `Llama-2-7b-chat.Q4_K_M.gguf` or `Mistral-7B-Instruct-v0.2.Q4_K_M.gguf`) and rename it to `model.gguf`.
Installation
Clone or Download this repository.
Install the expected dependencies:
```bash
   pip install -r requirements.txt
   ```
Note: Ensure you also have `PyPDF2` and `chromadb` installed, as they are utilized by the RAG module in this project!
```bash
   pip install PyPDF2 chromadb
   ```
Download Model: Place your downloaded `.gguf` file inside the root directory and rename it to `model.gguf`.
Usage/How to Run
Train RL Model (Optional): If you don't already have `ppo_tutor_model.zip`, you can run `python rl_tutor.py` to train one. A pre-trained model might already be included.
Start the Web Interface:
```bash
   streamlit run app.py
   ```
Your default web browser will open (usually `http://localhost:8501`), giving you access to the interactive tutor AI and the sidebar to upload document PDFs!
Project Structure
`app.py`: Main Streamlit web frontend. Unifies RL metrics, RAG interface, and LLM communication.
`rag_handler.py`: PDF processing, character-based chunking, and persistent ChromaDB integration.
`rl_tutor.py`: Custom Gymnasium environment tracking student fatigue, typing delay, and response lengths alongside Stable-Baselines3 PPO logic.
`test_rag.py`: Standalone script for testing the ChromaDB RAG chunk adding/query generation.
`requirements.txt`: Initial python module dependencies list.
