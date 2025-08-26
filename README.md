# Automatic Fine-Tuning Pipeline for LLMs

This project demonstrates an end-to-end pipeline for automatically fine-tuning a Large Language Model (LLM) on a custom corpus of documents. The goal is to create a model that is an expert on the provided text, capable of answering specific questions with high accuracy and relevance.

---

## Key Features

* **Automated Content Extraction:** Reads and processes multiple PDF documents, handling text extraction and segmentation.
* **Instruction Dataset Generation:** Utilizes a base LLM to automatically create a high-quality instruction-following dataset (in Alpaca/ShareGPT style) from the source documents.
* **Efficient Fine-Tuning:** Employs **QLoRA** (Quantized Low-Rank Adaptation) to fine-tune a small open-source model efficiently on a Google Colab T4 GPU, reducing VRAM usage significantly.
* **Comparative Evaluation:** Compares the performance of the base model against the fine-tuned model on a series of prompts to showcase the improvements.

---

## Technical Approach

This project explores two distinct methods for building the fine-tuning pipeline.

### Method 1: End-to-End Fine-Tuning

This approach focuses on a direct, hands-on implementation of each pipeline stage.

1.  **Data Ingestion:** A custom script reads three PDF documents, extracts all text, and segments the content into logical chunks.
2.  **Dataset Creation:** A prompt is designed to instruct a separate LLM to generate a question-and-answer pair for each segment of text. This process is fully automated, creating a new dataset from scratch without manual labeling.
3.  **Model Fine-Tuning:** The generated dataset is used to fine-tune a Gemma or Llama family model. The **`unsloth`** library is used to apply QLoRA, which trains only a small number of new parameters while keeping the original model's weights frozen. This makes the training process extremely fast and memory-efficient.
4.  **Performance Evaluation:** The base model and the newly fine-tuned model are put to the test. A series of questions based on the source documents are posed to both models to compare their ability to recall and synthesize information.

### Method 2: LlamaIndex Integration

This method demonstrates a more streamlined approach by leveraging the **LlamaIndex** framework.

1.  **Document Ingestion:** LlamaIndex's built-in document loaders are used to ingest the same PDF files. The framework automatically handles text splitting and embedding.
2.  **Fine-Tuning Integration:** While LlamaIndex is powerful for Retrieval-Augmented Generation (RAG), its data-handling capabilities are leveraged to prepare the fine-tuning dataset. The core fine-tuning logic from Method 1 is integrated with the LlamaIndex-processed data.
3.  **Enhanced Querying (RAG + Fine-Tuning):** This hybrid approach highlights how fine-tuning can be combined with a robust retrieval system. The fine-tuned model has a deeper understanding of the documents, while the LlamaIndex backend can still retrieve the exact source context, leading to more accurate and reliable answers.

---

## How to Run

1.  **Prerequisites:** You will need a Google account to access Google Colab. The notebook is configured to run on a T4 GPU, which is available for free in Colab.
2.  **Open the Notebook:** Click the "Open in Colab" badge at the top of the `Automatic_Fine_Tuning_Pipeline_LLM.ipynb` file in this repository.
3.  **Run All Cells:** Once the notebook is open, select `Runtime > Run all` from the top menu. The notebook is designed to be self-contained and will execute all steps of the pipeline sequentially, from data extraction to model evaluation.

---

##  Repository Contents

* `README.md`: This file, providing an overview of the project.
* `Automatic_Fine_Tuning_Pipeline_LLM.ipynb`: The main Google Colab notebook containing all the code for both fine-tuning methods.

---

## Contact

For any questions or feedback, feel free to reach out.

Dhinesh Harikrishnan
M.S in Electrical Engineering and Embedded Systems
Email: hkdhinesh@gmail.com
