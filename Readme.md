# Retrieval-Augmented Generation (RAG) for Insurance Query Processing

## Table of Contents
- [Introduction](#introduction)
- [Problem Statement](#problem-statement)
- [Objectives](#objectives)
- [System Architecture](#system-architecture)
- [Technologies Used](#technologies-used)
- [Setup Instructions](#setup-instructions)
- [Usage](#usage)
- [Example Queries](#example-queries)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)

---

## **Introduction**
This project implements a **Retrieval-Augmented Generation (RAG) pipeline** to provide **fact-based responses** to insurance-related queries. It combines **document retrieval** using **semantic search** and **OpenAI's GPT model** to generate responses based on real insurance policy documents.

The system is designed to help customers, agents, and insurance professionals quickly find **accurate and verified** answers about insurance policies, claim conditions, and coverage details.

---

## **Problem Statement**
Insurance policies are often complex, lengthy, and difficult to understand. Existing AI models can generate misleading responses due to the lack of factual grounding. This project solves these challenges by:
- Retrieving **actual** policy documents before answering a query.
- Generating responses **based on retrieved text** rather than just the AI's knowledge.
- Ensuring **contextually relevant** and **factually correct** information retrieval.

---

## **Objectives**
1. **Improve accuracy** in answering insurance-related queries.
2. **Enhance transparency** by providing document-backed responses.
3. **Reduce AI hallucinations** by retrieving relevant text from stored policy documents.
4. **Ensure scalability** for handling large datasets and multiple queries.
5. **Enable fast and efficient retrieval** through optimized search techniques.

---

## **System Architecture**
The project follows a **four-step pipeline**:

1. **Document Processing & Storage**
   - Insurance policy PDFs are loaded and **split into chunks**.
   - Text embeddings are created using OpenAI's `text-embedding-ada-002` model.
   - Embeddings are stored in **ChromaDB** for fast semantic search.

2. **Query Processing**
   - User queries are converted into vector embeddings.
   - **MMR (Maximal Marginal Relevance) search** is used to retrieve **diverse, relevant** policy snippets.
   - **Cross-encoder reranking** improves retrieval accuracy.

3. **Retrieval-Augmented Generation (RAG)**
   - Retrieved policy documents are formatted into a structured prompt.
   - The **GPT model** is used to generate a response based on retrieved documents.

4. **Response Generation**
   - The model generates **clear, human-readable** answers.
   - **Citations and document references** are provided for verification.

---

## **Technologies Used**
| Component | Technology |
|-----------|-----------|
| **LLM Model** | OpenAI's `gpt-4` or `gpt-3.5-turbo` |
| **Embedding Model** | `text-embedding-ada-002` |
| **Vector Database** | ChromaDB |
| **Document Processing** | PyPDF, LangChain |
| **Retrieval Method** | MMR (Maximal Marginal Relevance) Search |
| **Reranking Model** | `BAAI/bge-reranker-base` |
| **Frameworks** | LangChain, FastAPI (optional) |
| **Programming Language** | Python |

---

## **Setup Instructions**
Follow these steps to install and run the project.

### **1. Clone the Repository**
```sh
git clone https://github.com/ivineettiwari/Semantic-Spotter-prj.git
cd Semantic-Spotter-prj
```

### **2. Install Dependencies**
```sh
pip install -r requirements.txt
```

### **3. Set Up API Key**
Create an `API_Key.txt` file and store your OpenAI API key:
```sh
echo "your-openai-api-key" > API_Key.txt
```

Alternatively, set it as an environment variable:
```sh
export OPENAI_API_KEY="your-openai-api-key"
```

### **4. Prepare Data**
- Place all **insurance policy PDFs** inside the `Policy_Documents/` folder.
- The system will process these documents automatically.

### **5. Run the Application**
```sh
python main.py
```

---

## **Usage**
### **1. Running a Query**
To test the system, run:
```python
query = "What is the life insurance coverage for disability?"
response = rag_chain.invoke(query)
print(response)
```

### **2. Retrieve Relevant Documents**
```python
retriever = get_retriever(50)
retrieved_docs = retriever.invoke("What happens if a person dies in an accident without wearing a seatbelt?")
for doc in retrieved_docs:
    print(doc.page_content[:300])  # Preview first 300 characters
```

---

## **Example Queries**
### **General Insurance Queries**
- "Can a 100-year-old person apply for term insurance?"
- "What are the key benefits of life insurance?"
- "How does accidental death impact claim settlement?"

### **HDFC Insurance Queries**
- "What is the eligibility criteria for HDFC group insurance?"
- "What are the benefits of HDFC Sampoorna Jeevan insurance?"
- "Explain HDFC Life Sanchay Plus Life Long Income Option."

### **Legal & Compliance Queries**
- "Does life insurance cover disability?"
- "What are the conditions for claim rejection in accidental death?"
- "What happens if a claim is filed after the policyholder's death without documentation?"

---

## **Future Enhancements**
### **1. Hybrid Search (Vector + Keyword-Based)**
- Integrate **BM25 keyword search** alongside **vector-based retrieval** for better accuracy.

### **2. Real-Time Document Updates**
- Allow uploading new **policy documents dynamically** without rebuilding the vector index.

### **3. Response Ranking & Confidence Scoring**
- Display **relevance scores** alongside retrieved documents.
- Rank responses based on **model confidence**.

### **4. API Deployment (FastAPI/Flask)**
- Convert this project into an API service for **integration into customer support chatbots**.

### **5. Multi-Modal Support**
- Process scanned PDFs with **OCR-based text extraction**.

---

## **Contributing**
We welcome contributions! To contribute:
1. Fork this repository.
2. Create a new branch (`feature-branch`).
3. Commit your changes and push them.
4. Create a Pull Request.