# FirstAid_RAG (Retrieval-Augmented Generation)

## Overview
The **FirstAid RAG** project is a Retrieval-Augmented Generation system tailored for answering medical-related queries using contextual information. The system combines text retrieval and generation capabilities to provide accurate and concise answers. It uses a Hugging Face-based large language model (LLM) with FAISS for efficient similarity-based search over a collection of medical documents.

---

## Features
- **Document Ingestion**: Load and preprocess documents using `langchain`.
- **Text Chunking**: Splits documents into manageable chunks for efficient retrieval.
- **FAISS Vector Store**: Embeds chunks and stores them in a FAISS vector database for semantic similarity search.
- **Custom Prompting**: Generates responses using a carefully crafted prompt template.
- **Real-Time Interaction**: Accepts user queries in real time and provides responses.
- **Response Cleaning**: Ensures answers are well-formatted, concise, and free of artifacts.

---

## Setup
1. **Set Hugging Face API Key**:
   Add your Hugging Face API key securely via Colab's `userdata` or environment variables:

   ```python
   API_KEY = userdata.get('HF_TOKEN')
   os.environ["HUGGINGFACEHUB_API_TOKEN"] = API_KEY
   ```

2. **Document Loading**:
   Use `DirectoryLoader` from `langchain_community` to load and preprocess your documents.

3. **FAISS Vector Store**:
   - Embed document chunks using `HuggingFaceEmbeddings`.
   - Store embeddings in FAISS for fast similarity-based retrieval.

4. **Model Configuration**:
   Configure the LLM using Hugging Face's hosted endpoint:

   ```python
   llm_model = HuggingFaceEndpoint(
       repo_id="mistralai/Mistral-7B-v0.1",
       max_length=50,
       temperature=0.5
   )
   ```

---

## Usage
### Run the System
1. **Start the Query Loop**:
   Execute the code to initiate a query loop where users can input medical-related questions.

2. **Input Queries**:
   Enter queries like `What is first aid?` and get context-driven responses.

3. **Exit the Loop**:
   Type `thank you` to exit the query session.

---

## Code Highlights
1. **Text Chunking**:
   ```python
   text_splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=400)
   text_doc = text_splitter.split_documents(text)
   ```

2. **Custom Prompt**:
   ```python
   prompt = """Use the following pieces of information to answer the user's question.
   If you don't know the answer, just say that you don't know, don't try to make up an answer.
   And rephrase the answer into not more than 50 tokens.

   Context: {context}
   Question: {question}
   """
   ```

3. **Response Cleaning**:
   Removes unwanted patterns and ensures proper formatting:
   ```python
   def clean_response(output):
       # Remove artifacts and clean text
       ...
   ```

---

## Key Dependencies
- **LangChain**: For text processing and chain management.
- **FAISS**: Vector similarity search.
- **Hugging Face**: Large language model hosting.

---

## Future Enhancements
- Expand the dataset to include more comprehensive medical documents.
- Integrate additional models for multilingual support.
- Deploy the system as a web or mobile application for better accessibility.

---

## License
This project is open-source and available under the [MIT License](LICENSE).

