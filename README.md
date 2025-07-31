# multi-modal-rag-system
"A RAG system that answers questions from PDFs using both text and image analysis with LLaVA and Tesseract."
# Multi-Modal RAG System for Comprehensive Document Analysis

This project is an advanced Retrieval-Augmented Generation (RAG) system built in a Google Colab notebook. It's designed to provide a comprehensive Question-Answering experience for any user-uploaded PDF document.

Unlike traditional text-only RAG systems, this project incorporates a hybrid multi-modal approach, enabling it to understand and answer questions about both the **text** and the **visual content** (maps, figures, diagrams) within a document.

## ✨ Features

-   **Multi-Modal Document Processing:** Ingests PDF files and intelligently extracts both text and embedded images.
-   **Hybrid Vision Analysis:** Uses a powerful combination of:
    -   **LLaVA:** A vision-language model to provide high-level descriptions and context for images.
    -   **Tesseract OCR:** To extract and read specific text (labels, titles, legends) directly from the images.
-   **Fact-Grounded Answers:** Employs the RAG architecture to retrieve relevant context before generating an answer, significantly reducing "hallucinations" and ensuring responses are based on the source document.
-   **Interactive Q&A:** Provides a simple command-line interface to ask questions in natural language and receive detailed answers.

## 🛠️ Tech Stack & Architecture

The system is built using a modern, open-source AI stack, orchestrated with LangChain.

-   **Core Framework:** LangChain
-   **PDF & Image Extraction:** PyMuPDF
-   **Vision Model (Description):** LLaVA (`llava-hf/llava-1.5-7b-hf`)
-   **OCR Engine (Text Extraction):** Tesseract
-   **Language Model (Generation):** Qwen (`Qwen/Qwen1.5-1.8B-Chat`)
-   **Embedding Model:** SentenceTransformers (`all-MiniLM-L6-v2`)
-   **Vector Store:** FAISS (Facebook AI Similarity Search)
-   **Core AI Libraries:** Hugging Face Transformers, PyTorch
-   **Environment:** Google Colab

The workflow is as follows:
1.  **Ingest:** A PDF is uploaded.
2.  **Extract:** Text and images are extracted on a per-page basis.
3.  **Analyze & Combine:** Images are described by LLaVA and read by Tesseract. This visual information is converted to text and merged with the original page text.
4.  **Index:** The combined rich text is chunked, embedded, and stored in a FAISS vector database.
5.  **Retrieve & Generate:** A user's query retrieves the most relevant chunks, which are then passed to the Qwen model to generate a final answer.

## 🚀 How to Use

1.  **Open in Colab:** Open the `Last_Attempt.ipynb` notebook in Google Colab.
2.  **Select GPU Runtime:** For the models to run efficiently, you must use a GPU. Go to **Runtime** -> **Change runtime type** and select **T4 GPU** from the dropdown menu.
3.  **Run Installation & Imports:** Execute the first two cells to install all necessary libraries and import them.
4.  **Upload a PDF:** Run the file upload cell (Cell 3) and select a PDF document from your computer.
5.  **Run Sequentially:** Execute the remaining cells in order. The cells will:
    -   Load the LLaVA and Qwen models (this may take a few minutes).
    -   Process your PDF, including image analysis.
    -   Build the vector database.
    -   Define the Q&A pipeline.
6.  **Ask Questions:** The final cell will start an interactive chat loop. Enter your questions about the document in the prompt and press Enter. Type `exit` to end the session.

## 🔮 Future Improvements

-   **User Interface:** Wrap the application in a simple web UI using Gradio or Streamlit for easier, more visual interaction.
-   **Conversational Memory:** Implement a memory buffer to allow for context-aware follow-up questions (e.g., "Can you tell me more about that?").
-   **Source Citation:** Modify the pipeline to cite the specific page number(s) from which the answer was derived, increasing user trust and verifiability.

## 📄 License

This project is licensed under the MIT License.
