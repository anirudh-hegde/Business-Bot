# RAG-Based Technical Support Bot

## Project Overview
This project implements a **Retrieval-Augmented Generation (RAG)** model for a technical support chatbot. It combines the power of Pinecone for semantic search, Sentence-Transformer for embedding generation, and Google's Gemini AI for content generation to provide enriched responses to user queries.

The system is designed to retrieve relevant documents from a technical support dataset, augment the retrieved information, and use a generative AI model to generate precise and contextually appropriate responses.

---

## Key Features
1. **Retrieval-Augmented Generation**:
   - Retrieves relevant technical support responses from a Pinecone vector database.
   - Uses Google's Gemini AI to provide enriched, context-aware answers to user queries.

2. **Semantic Search**:
   - Embeddings generated with the `SentenceTransformer` (`all-MiniLM-L6-v2`) model enable precise semantic search in the Pinecone index.

3. **Domain-Specific Optimization**:
   - The technical support dataset includes domain-specific data, ensuring the model generates accurate and reliable answers for common customer issues.

4. **Scalable Indexing**:
   - Supports batch indexing for large datasets, making it suitable for enterprise-scale applications.

5. **Dynamic Index Management**:
   - Deletes and re-initializes Pinecone indexes dynamically for seamless operation and testing.

---

## Workflow

1. **Dataset Preparation**:
   - Load a technical support dataset (`tech_support_dataset.csv`) containing columns `Customer_Issue` and `Tech_Response`.
   - Each entry is assigned a unique identifier (`id`) for indexing.

2. **Embedding Generation**:
   - Use `SentenceTransformer` to encode `Customer_Issue` into 384-dimensional embeddings.

3. **Pinecone Integration**:
   - The embeddings and metadata (e.g., `Tech_Response` and `Customer_Issue`) are stored in a Pinecone vector database.
   - Supports real-time querying and document retrieval.

4. **Query Handling**:
   - Generate embeddings for user queries.
   - Retrieve the most relevant technical responses from Pinecone.

5. **Content Generation**:
   - Augment retrieved responses using a prompt and feed them into Gemini AI.
   - Generate a final enriched response to the user query.

---

## Project Components

### 1. **Code Modules**
- **`delete_index()`**: Deletes the existing Pinecone index if it exists.
- **`initialize_index()`**: Initializes a new Pinecone index with specified parameters.
- **`generate_embedding()`**: Encodes text into 384-dimensional embeddings using `SentenceTransformer`.
- **`index_dataset()`**: Indexes the dataset into the Pinecone vector database in batches for scalability.
- **`query_index()`**: Retrieves the top-k relevant documents from the Pinecone index based on a query.
- **`generate_enriched_response()`**: Combines retrieved documents with Gemini AI for generating enriched responses.

### 2. **Technologies Used**
- **Google Generative AI (Gemini)**: For generating content based on retrieved responses.
- **Pinecone**: For efficient and scalable vector search.
- **Sentence-Transformers**: For generating semantic embeddings.
- **Python**: Core programming language for implementation.
- **Pandas**: For dataset handling.

---

## Dataset Structure
The dataset (`tech_support_dataset.csv`) should contain the following columns:
- **`Customer_Issue`**: Descriptions of customer problems or questions.
- **`Tech_Response`**: Predefined technical solutions or responses to customer issues.

An additional column `id` is generated dynamically to uniquely identify each entry for indexing in Pinecone.

---

## How to Run the Project

### 1. Prerequisites
- Python 3.8+
- Install dependencies:
  ```bash
  pip install google-generativeai pinecone-client sentence-transformers pandas
  ```
- API Keys:
  - Pinecone: Set your `PINECONE_API_KEY` and `PINECONE_ENV` variables.
  - Gemini AI: Set your `api_key` in the `genai.configure()` function.

### 2. Dataset Preparation
Ensure your dataset (`tech_support_dataset.csv`) is properly formatted and accessible.

### 3. Execute the Script
Run the Python script to:
1. Delete and initialize the Pinecone index.
2. Index the dataset into Pinecone.
3. Query the index using a user-provided question.
4. Generate a response using Gemini AI.

### Example Usage
```bash
python tech_support_bot.py
```
- Enter your query when prompted, and the bot will generate a detailed, enriched response.

---

## Future Improvements
1. **Enhanced Retrieval**:
   - Implement hybrid retrieval combining dense embeddings and keyword-based search.
2. **Dataset Expansion**:
   - Add more domain-specific queries and responses for better fine-tuning.
3. **Model Optimization**:
   - Fine-tune the embedding model (`SentenceTransformer`) on the technical support dataset.
4. **Re-ranking**:
   - Introduce a contextual re-ranking step for retrieved documents before feeding them into the generative model.

---

## License
This project is licensed under the MIT License. See the LICENSE file for details.

---

## Acknowledgments
- [Google Generative AI (Gemini)](https://ai.google/)
- [Pinecone](https://www.pinecone.io/)
- [Hugging Face Sentence-Transformers](https://www.sbert.net/)
