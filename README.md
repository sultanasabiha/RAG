# **RAG QA Bot Documentation**

## **Overview**
The **RAG QA Bot** is a **Streamlit-based** application that allows users to upload documents, index their contents, and ask questions using Retrieval-Augmented Generation (RAG). It integrates the **LlamaIndex** library to connect large language models (LLMs) with document retrieval capabilities, enabling context-aware responses. The app uses **Pinecone** as the vector store for document embeddings and a **Hugging Face LLM** model for generating responses.

---

## **Features**
- **Document Upload**: Users can upload files, which are then processed and split into smaller chunks for indexing.
- **Vector Store Initialization**: The app integrates with Pinecone to store document embeddings and enables efficient document retrieval.
- **Generative AI Responses**: A Hugging Face LLM is used to generate responses based on user queries and relevant document segments retrieved ny LLamaIndex.
- **Real-Time Q&A**: Users can input questions, and the app retrieves relevant information from the documents and generates responses in real-time.
- **Conversation History**: The chat history is maintained during the session, allowing users to scroll through their interactions.


---

## **Installation Guide**

### **Pre-requisites**
- Python 3.8+
- Packages: `streamlit`, `transformers`, `llama-index`, `torch`, `llama_index-embeddings-huggingface`,`pinecone[grpc]`, `llama_index-vector_stores-pinecone`,`accelerate`,`bitsandbytes`,`llama_index-llms-huggingface`
  
- API Keys for Hugging Face and Pinecone:
  - **Hugging Face API Key** for using the LLM
  - **Pinecone API Key** for vector store management

### **Step 1: Clone the Repository**
Clone the application repository (or download the code):

```bash
git clone <[repository-link](https://github.com/sultanasabiha/RAG)>
cd <RAG>
```

### **Step 2: Install Dependencies**
Install the required Python packages using `pip`:

```bash
pip install -r requirements.txt
```


### **Step 3: Set Up Environment Variables**
You need to set up the following environment variables for the app to work:

1. **Hugging Face API Key**: `HF_TOKEN`
2. **Pinecone API Key**: `PC_API_KEY`

You can add these to your google colab secrets and enable access to the notebook to readily set the environment.

### **Step 4: Run the Application**
Run the Streamlit app by executing the following command:

```bash
streamlit run app.py
```

### **Step 5: Expose Locally with LocalTunnel **
If you want to share the app with others remotely, you can expose the local server using LocalTunnel. First, ensure LocalTunnel is installed globally:

```bash
npm install -g localtunnel
```

Then run the app and start LocalTunnel:

```bash
streamlit run app.py
npx localtunnel --port 8501
```

You will get a public URL that can be shared with others to access the app remotely.

---

## **Application Workflow** 

### **1. Initialization**
- The app starts by configuring the page with a header and options for users to clear the conversation.
- API keys are loaded from the environment for Hugging Face and Pinecone.

### **2. File Upload**
- Users can upload a document (e.g., a PDF or text file) via the file uploader.
- The uploaded file is saved in the server, and its content is read and chunked into smaller sections using `SimpleDirectoryReader`.

### **3. Vector Store Initialization**
- Once a file is uploaded, a Pinecone vector store is initialized. 
- The app checks if a vector index with the given name exists in Pinecone. If not, a new index is created.
- Document embeddings are generated using Hugging Face’s embeddings model and stored in Pinecone.

### **4. LLM Selection**
- A Hugging Face model (`mistralai/Mistral-7B-Instruct`) is used for generating responses.
- The model is loaded in quantized mode (4-bit) to save memory, making it efficient for GPU use.

### **5. Q&A Interaction**
- Users can input a question via the chat interface.
- The app retrieves relevant document segments from Pinecone and displays them in the sidebar.
- Using the selected LLM, the app generates a response, streaming it back to the user in real-time.
- Both the query and the generated response are stored in the session state for conversation history.

### **6. Clear Conversation**
- Users can clear the chat history using a button in the sidebar, resetting the stored messages.



---

## **Usage**

1. **Upload a Document**: 
   - Select a file to upload, and the app will process and index it.
2. **Ask a Question**: 
   - Type a question in the input box, and the app will retrieve relevant information from the document and provide an AI-generated answer.
3. **Review Document Segments**:
   - The app will display the relevant document sections used to answer your question in the sidebar.

---

## **System Requirements**
- **GPU Support**: The app is optimized for environments with GPU support to enable efficient model loading and inference.
- **API Keys**: Ensure that valid Hugging Face and Pinecone API keys are set up.

---

## **Troubleshooting**

### **Issue: Bad Gateway 202.**
- This error typically occurs when the local server is not responding correctly through LocalTunnel, leading to a communication issue.
- Refresh the page: The issue may occur intermittently due to LocalTunnel connection issues. A simple page refresh might resolve it.
- Restart LocalTunnel: Close and reopen the LocalTunnel session to reset the connection.

### **Issue: API keys are missing or invalid.**
- Verify that the environment variables for `HF_TOKEN` and `PC_API_KEY` are correctly set.

### **Issue: No response generated for a question.**
- Make sure that the document is successfully uploaded and indexed.
- Verify that the Pinecone service is running and accessible.

---
## RAG Backend Usage Examples:
![Backend queries](images/Screenshot%20134.png)
![Backend queries](images/Screenshot%20135.png)


## QA Bot Usage Examples:

![APP start page](images/Screenshot%20130.png)
![APP start page](images/Screenshot%20131.png)
![Querying](images/Screenshot%20132.png)
![Querying](images/Screenshot%20137.png)
![Querying](images/Screenshot%20138.png)
