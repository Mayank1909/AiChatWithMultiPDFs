# 📚 Chat with Multiple PDFs AI 🤖

Welcome to the **Chat with Multiple PDFs AI** project! This Streamlit application allows you to upload several PDF documents and ask questions based on their combined content. It leverages the power of **Google's Gemini** models through the **LangChain** framework to perform advanced Retrieval-Augmented Generation (RAG).

## ✨ Features

* **Multi-PDF Support:** Upload and process multiple PDF files simultaneously.
* **Gemini Integration:** Uses the **Gemini-2.5 Flash** model (or similar) for intelligent, contextual, and fast question-answering.
* **LangChain RAG Pipeline:** Implements a robust RAG workflow using:
    * **PyPDF2** for text extraction.
    * **RecursiveCharacterTextSplitter** for optimal text chunking.
    * **GoogleGenerativeAIEmbeddings** for creating vector representations.
    * **FAISS** (Facebook AI Similarity Search) for fast and efficient vector storage and retrieval.
* **Streamlit Interface:** A clean, user-friendly web interface for file uploading and chatting.
* **Contextual Answers:** Retrieves the most relevant information from the PDFs to provide accurate, non-hallucinated answers.

## 🛠️ Installation

### Prerequisites

* Python 3.8+
* A **Gemini API Key** from [Google AI Studio](https://ai.google.dev/gemini-api/docs/api-key).

### Setup Steps

1.  **Clone the Repository:**

    ```bash
    git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
    cd your-repo-name
    ```

2.  **Create a Virtual Environment (Recommended):**

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use: .\venv\Scripts\activate
    ```

3.  **Install Dependencies:**

    You can generate a `requirements.txt` file from your code, or manually list the libraries:
    
    * *Assuming your libraries are:* `streamlit`, `PyPDF2`, `langchain`, `langchain-google-genai`, `langchain-community`, `python-dotenv`, `faiss-cpu`.

    ```bash
    pip install -r requirements.txt
    # If you don't have a requirements.txt, use:
    # pip install streamlit PyPDF2 langchain langchain-google-genai langchain-community python-dotenv faiss-cpu
    ```

4.  **Set up your API Key:**

    Create a file named **`.env`** in the root directory of the project and add your API key. The LangChain components automatically look for `GEMINI_API_KEY` or `GOOGLE_API_KEY`.

    ```dotenv
    # .env file content
    GEMINI_API_KEY="YOUR_API_KEY_HERE" 
    ```

## 🚀 Usage

1.  **Run the Streamlit Application:**

    ```bash
    streamlit run your_app_name.py 
    # (e.g., streamlit run chat_pdf.py)
    ```
    
    The application will open in your web browser (usually at `http://localhost:8501`).

2.  **Upload and Process:**
    * Navigate to the **sidebar** (Menu).
    * Use the **File Uploader** to select one or more PDF files.
    * Click the **"Submit & Process"** button.
    * Wait for the "Processing..." spinner to finish and see the "Done" message. This step extracts text, chunks it, embeds the chunks, and creates the local `faiss_index` vector store.

3.  **Ask Questions:**
    * Enter your question in the main text box, for example: "What are the main topics discussed in all the documents?"
    * The AI will search the vector store for relevant context and use the Gemini model to generate an answer.

## ⚙️ Project Structure (Relevant to your code)

The core logic is handled by a standard LangChain RAG pipeline:

1.  **`get_pdf_text(pdf_docs)`:** Extracts raw text from the uploaded PDFs.
2.  **`get_text_chunks(raw_text)`:** Splits the long text into smaller, overlapping chunks suitable for embedding.
3.  **`get_vector_store(text_chunks)`:** Generates embeddings using `GoogleGenerativeAIEmbeddings` and stores them in a local **FAISS** index.
4.  **`get_conversational_chain()`:** Sets up the **Question-Answering chain** (`load_qa_chain`) using the **`ChatGoogleGenerativeAI`** model and a custom `PromptTemplate`.
5.  **`user_input(user_question)`:** Performs a similarity search on the FAISS index with the user's question, retrieves context, and invokes the QA chain to get the final response.

---


## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
