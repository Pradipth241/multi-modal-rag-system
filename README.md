# Multi-Modal RAG System for Comprehensive Document Analysis

This project is an advanced Retrieval-Augmented Generation (RAG) system built in a Google Colab notebook. It's designed to provide a comprehensive Question-Answering experience for any user-uploaded PDF document, with a special focus on older, scanned, or complex files.

A key challenge with many historical or archived documents is that the text is not selectable and exists only as part of an image. Standard text extraction fails on these files, and traditional OCR can struggle with degraded quality. This system is specifically designed to overcome that limitation.

## ✨ Features

-   **Handles Both Modern and Scanned PDFs:** Processes both digitally native PDFs (with selectable text) and older, scanned PDFs where pages are essentially images.
-   **Multi-Modal Document Processing:** Ingests PDF files and intelligently extracts both text layers and embedded images.
-   **Hybrid Vision Analysis:** For pages or figures that are images, the system uses a powerful combination of:
    -   **LLaVA:** A vision-language model to provide high-level descriptions and context for the image (e.g., "This is a military map showing troop movements").
    -   **Tesseract OCR:** To extract and read specific text (labels, titles, legends) directly from the images, even when it's not in a standard text layer.
-   **Fact-Grounded Answers:** Employs the RAG architecture to retrieve relevant context before generating an answer, significantly reducing "hallucinations" and ensuring responses are based on the source document.
-   **Interactive Q&A:** Provides a simple command-line interface to ask questions in natural language and receive detailed answers.

## 💡 Solving the Scanned Document Problem

Many older PDFs are simply collections of scanned images. A standard tool cannot "read" this content because there is no underlying text layer. While Tesseract OCR is a powerful tool for reading text in images, it can be insufficient on its own for full comprehension.

This system solves the problem with a two-step hybrid approach:

1.  **Contextual Understanding with LLaVA:** The LLaVA vision model first analyzes the image to understand *what it is*. It provides a high-level summary, such as identifying a map, a table, or a diagram. This gives the system crucial context that pure OCR cannot provide.
2.  **Detailed Text Extraction with Tesseract:** Tesseract then performs its specialized task of extracting all readable characters from the image.

By combining LLaVA's contextual summary with Tesseract's raw text extraction, the system builds a rich, machine-readable understanding of image-based pages, allowing you to ask questions about documents that other systems would find unreadable.

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

## 🚀 How to Use

1.  **Open in Colab:** Open the `.ipynb` notebook in Google Colab.
2.  **Select GPU Runtime:** For the models to run efficiently, you must use a GPU. Go to **Runtime** -> **Change runtime type** and select **T4 GPU**.
3.  **Run Installation & Imports:** Execute the first few cells to install all necessary libraries and import them.
4.  **Upload a PDF:** Run the file upload cell and select a PDF document from your computer. This can be a modern or a scanned, image-based PDF.
5.  **Run Sequentially:** Execute the remaining cells in order to load the models, process the document, and build the vector database.
6.  **Ask Questions:** The final cell will start an interactive chat loop. Enter your questions about the document in the prompt and press Enter. Type `exit` to end the session.

## 🔮 Future Improvements

-   **User Interface:** Wrap the application in a simple web UI using Gradio or Streamlit.
-   **Conversational Memory:** Implement a memory buffer to allow for context-aware follow-up questions.
-   **Source Citation:** Modify the pipeline to cite the specific page number(s) from which the answer was derived.

## 📄 License

This project is licensed under the MIT License.
