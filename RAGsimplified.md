# Understanding RAG Systems

## 1. **How RAG Works**

Think of **Retrieval Augmented Generation (RAG)** as a highly intelligent library system that combines search and knowledge generation to provide precise and contextual answers.

Here’s how it works:  

1. **Organize and Index Your Library**:
   - Just like categorizing and indexing books in a library, all your documents are processed and converted into searchable embeddings stored in a **vector database**.

2. **Retrieve Relevant Information**:
   - When someone asks a question, the system searches the "library" for the most relevant pages or sections (chunks) based on the query’s meaning, not just the exact words.

3. **Generate an Answer**:
   - The retrieved pages are passed to a **language model (LLM)**, which uses them as a reference to:
     - Understand the question better.
     - Formulate a detailed and accurate answer.

4. **Deliver a Contextual Response**:
   - The answer combines the **language model’s reasoning ability** with the **specific information retrieved** to provide both depth and accuracy.

---

### **Analogy**
Imagine asking a librarian about a topic:
- The librarian first finds the most relevant books and pages in the library.
- Then, instead of just showing you the books, they read and summarize the content, combining it with their own knowledge to provide a clear, well-informed response.

---

### **Why is RAG Important?**
- Enables **personalized and accurate answers** using specific context from documents.
- Combines **retrieval (precision)** and **generation (creativity)** for more reliable AI-powered solutions.
- Scales well for large knowledge bases or dynamic datasets.

---

## 2. **Vector Databases**

### **What Are Vector Databases?**
Think of a **vector database** as a tool that organizes information based on meaning rather than exact words. It works by converting pieces of text, images, or other data into vectors—numerical points in a high-dimensional space. 

In this space:
- **Similar content appears closer together.**
- **Different or unrelated content appears farther apart.**

#### **Example:**
- **"The cat sat on the mat"** and **"A kitten rests on the rug"** would be represented as close points in the vector space because they have similar meanings.
- **"Python is a programming language"** would be far from both because it has a completely different meaning.

---

### **Why Use Vector Databases?**

#### **Limitations of Traditional Databases**:
- They rely on exact matches (e.g., finding records with the exact words or phrases).
- Cannot handle semantic queries (searching by meaning instead of specific terms).

#### **Advantages of Vector Databases**:
1. **Search by Meaning**:
   - Even if the user query doesn’t match the exact words in a document, the vector database can find relevant content based on its meaning.
   - Example: A query for *"feline on a carpet"* could retrieve documents about *"cat on a rug."*

2. **Semantic Similarity**:
   - Finds content that shares context or conceptual similarity, which is critical for tasks like document retrieval, recommendations, or question answering.

3. **High Performance**:
   - Optimized for fast searches even in massive datasets containing millions of vectors.

---

### **Key Use Cases for Vector Databases**:
- **Document Retrieval**: Finding relevant passages or answers from large knowledge bases.
- **Recommendation Systems**: Suggesting similar items based on user preferences.
- **Image/Video Search**: Locating media based on visual similarity.
- **AI-Powered Applications**: Enhancing RAG pipelines and chatbot functionality.

---

## 3. Document Processing & Chunking

### What is Chunking?

**Chunking** is the process of breaking down large documents into smaller, meaningful, and manageable pieces to make them easier for AI systems to process and retrieve relevant information.

Think of it like:
- Taking a textbook and dividing it into individual topics.
- Ensuring each piece can stand alone while still maintaining the original context.

#### **Recommended Chunking Parameters**

| **Course Type**      | **Chunk Size** | **Overlap** |
|-----------------------|----------------|-------------|
| Lecture Notes         | 512 tokens     | 15%         |
| Research Papers       | 256 tokens     | 20%         |
| QA Pairs              | 128 tokens     | 0%          |

---

### **Chunking Strategies**

#### **1. Fixed-Size Chunking**
- **What it is**: Dividing content into chunks of uniform size, regardless of content boundaries.  
  *Example*: Cutting a book into fixed sections of 500 words each.  
- **Pros**:
  - Simple to implement.
  - Ensures consistency across chunks.
- **Cons**:
  - Can disrupt context by cutting through sentences, paragraphs, or ideas.

#### **2. Semantic Chunking**
- **What it is**: Dividing content based on natural meaning or context, such as sentences, paragraphs, or sections.  
  *Example*: Splitting by topic headings or paragraphs in lecture notes.  
- **Pros**:
  - Retains the original context of the content.
  - Better for queries requiring contextual accuracy.
- **Cons**:
  - Requires additional processing (e.g., NLP techniques) to identify boundaries.

---

### **How to Choose the Right Chunking Strategy**
- **Fixed Size**:
  - Best for structured, uniform data (e.g., logs, repeated formats).
  - Use when simplicity and speed are more important than preserving context.
- **Semantic**:
  - Ideal for unstructured or complex content (e.g., research papers, lecture notes).
  - Use when meaning and relevance are critical.

---

## 4. **Embeddings: Converting Text to Numbers**

### **What Are Embeddings?**
Embeddings are numerical representations of words, sentences, or documents that capture their **meaning and relationships** in a mathematical form.

Think of embeddings as **translating text into lists of numbers**, where similar concepts have similar numbers.

#### **Example**:
```plaintext
"Dog"       → [0.2, 0.5, -0.1, ...]
"Puppy"     → [0.19, 0.48, -0.08, ...]
"Computer"  → [-0.5, 0.1, 0.8, ...]
```
- **Dog** and **Puppy** have nearly identical embeddings because they are related concepts.
- **Computer** has a very different embedding, reflecting its unrelated meaning.

---

### **Why Are Embeddings Important?**
1. **Capture Relationships**:  
   - Words with similar meanings are close to each other in the embedding space, enabling systems to understand relationships between concepts.
   - Example: "King - Man + Woman = Queen."

2. **Semantic Search**:  
   - Allows searching based on meaning, not exact words (e.g., finding “puppy” when querying “dog”).

3. **Core of AI Models**:  
   - Embeddings are the foundation for tasks like similarity search, classification, clustering, and many more.

---

### **How Are Embeddings Used?**
- **Search Engines**: Retrieve relevant documents or answers.
- **Chatbots**: Understand user queries and provide meaningful responses.
- **Recommendation Systems**: Find similar items or content based on embeddings.

---

## 5. **Retrieval: Finding Relevant Information**

### **How Retrieval Works**
Retrieval is the process of finding the most relevant information for a given query by comparing **meanings**, not just exact words. Here's how it works step by step:

1. **Convert the User's Question into Numbers**:  
   - The question is transformed into an **embedding** (a list of numbers representing its meaning).

2. **Search for Similar Chunks**:  
   - Compare the query embedding with embeddings of document chunks in a **vector database**.
   - Identify chunks that are closest in meaning.

3. **Return the Most Relevant Chunks**:  
   - Retrieve the top matches and use them as context for answering the query.

---

### **Analogy: Finding Books in a Library**
- **Traditional Search**:  
  Like using an index to find books based on exact words or phrases.  
  *Example*: Search for "Artificial Intelligence" and get results containing the exact phrase.

- **Vector Search**:  
  Like finding books on similar topics, even if the exact words differ.  
  *Example*: Search for "AI concepts" and get results about "Machine Learning," "Deep Learning," or "Neural Networks" because they are conceptually related.

---

### **Why Use Vector Retrieval?**
- **Handles Synonyms and Paraphrasing**: Finds relevant content even if the user's wording differs.
- **Context-Aware**: Retrieves chunks that match the meaning of the query, not just its keywords.
- **Faster and Scalable**: Efficiently searches large datasets for semantically similar information.

---

## 6. **Indexing: Organizing for Speed**

### **Why Indexing?**
- Speeds up search
- Groups similar content together  
- Think of it like a library catalog that makes finding books fast.

### **Types of Indexes**:
1. **Flat**: Compares all items (slow but precise).  
2. **Tree-based**: Narrows down search areas (faster).  
3. **Clustering**: Groups similar items (balances speed and accuracy).  

---

## 7. **End-to-End Workflow**

### **Processing Phase**:  
1. Break course materials into meaningful chunks.  
2. Convert chunks into embeddings using a pre-trained model.  
3. Store embeddings along with metadata in a vector database.  

### **Query Phase**:  
1. Convert the student’s question into an embedding.  
2. Search the vector database for similar chunks.  
3. Retrieve top `k` chunks and aggregate them into a coherent context.  
4. Pass the user query and retrieved context to an LLM.  
5. Use the LLM to generate a response grounded in the context.  
6. Return the formatted answer to the student.  

Remember: Understanding these concepts is crucial before implementation. Take time to experiment and visualize how each component works.

## 8. **Learning Resources**

### **Colab Notebooks**:  

1. [A simple RAG to answer Queries](https://www.aispaceship.io/docs/category/rag-application)
2. [Langchain notebooks - Building RAG chat app part1](https://python.langchain.com/docs/tutorials/rag/)
3. [Langchain notebooks - Building RAG chat app with History part2](https://python.langchain.com/docs/tutorials/qa_chat_history/)
4. [Agentic RAG](https://langchain-ai.github.io/langgraph/tutorials/rag/langgraph_agentic_rag/)

### **YouTube Videos**

1. **[What is Langchain - 8 min video](https://youtu.be/1bUy-1hGZpI?si=S3A9dNfhPUlRqfQT)**
2. [Langchain crash course - 46 min video](https://youtu.be/nAmC7SoVLd8?si=IYXuihXeDgbnnDsR)
3. **[Langchain vs LangGraph - 9 min video](https://youtu.be/qAF1NjEVHhY?si=7BrHa6NOqtduNZ9d)**
4. There are a tone more but I know you guys won't watch any video so :)

