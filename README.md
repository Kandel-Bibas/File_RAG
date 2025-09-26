# File Reader RAG

A comprehensive Retrieval-Augmented Generation (RAG) application that allows users to upload PDF documents and interact with them through natural language queries. The application features both a modern Next.js frontend and a FastAPI backend, with an optional Streamlit interface for quick testing.

## 🚀 Features

- **PDF Upload & Processing**: Upload PDF documents and automatically extract text content
- **Vector Database**: Uses ChromaDB for efficient document storage and retrieval
- **AI-Powered Q&A**: Ask questions about your documents using OpenAI's GPT models
- **Real-time Streaming**: Get responses streamed in real-time for better user experience
- **Modern UI**: Clean, responsive interface built with Next.js and Tailwind CSS
- **Dual Interface**: Both web application and Streamlit demo available
- **Document Persistence**: Processed documents are stored and can be queried multiple times

## 🏗️ Architecture

### Backend (FastAPI)
- **FastAPI**: Modern, fast web framework for building APIs
- **ChromaDB**: Vector database for document storage and similarity search
- **OpenAI API**: GPT-4 for generating responses and text-embedding-ada-002 for embeddings
- **LangChain**: Document processing and text splitting utilities

### Frontend (Next.js)
- **Next.js 15**: React framework with App Router
- **TypeScript**: Type-safe development
- **Tailwind CSS**: Utility-first CSS framework
- **PDF Viewer**: Integrated PDF viewing component
- **Real-time Chat**: Interactive chat interface for document queries

### Streamlit Demo
- **Streamlit**: Quick demo interface for testing the RAG functionality
- **FAISS**: Alternative vector store implementation for comparison

## 📋 Prerequisites

- Python 3.8+
- Node.js 18+
- OpenAI API Key

## 🛠️ Installation

### 1. Clone the Repository
```bash
git clone <repository-url>
cd File_reader_RAG
```

### 2. Backend Setup
```bash
cd backend

# Install Python dependencies
pip install fastapi uvicorn python-multipart
pip install langchain langchain-community langchain-openai
pip install chromadb openai python-dotenv
pip install streamlit

# Set up environment variables
echo "OPENAI_API_KEY=your_openai_api_key_here" > .env
```

### 3. Frontend Setup
```bash
cd frontend

# Install dependencies
npm install

# Build the application
npm run build
```

## 🚀 Usage

### Option 1: Full Web Application

1. **Start the Backend Server**
```bash
cd backend
python main.py
```
The API will be available at `http://localhost:8000`

2. **Start the Frontend**
```bash
cd frontend
npm run dev
```
The web application will be available at `http://localhost:3000`

3. **Use the Application**
   - Navigate to `http://localhost:3000`
   - Click "Upload" to upload a PDF document
   - Click "Demo" to test with a sample document
   - Once uploaded, you can ask questions about the document

### Option 2: Streamlit Demo

```bash
cd backend
streamlit run streamlit.py
```

This will open a simple interface where you can:
- Upload a PDF file
- Ask questions about the document
- Get AI-generated responses

## 📁 Project Structure

```
File_reader_RAG/
├── backend/
│   ├── app/
│   │   └── services/
│   │       ├── pdf_processing.py    # PDF text extraction and processing
│   │       ├── vector_db.py         # ChromaDB operations
│   │       └── llm_query.py         # OpenAI API integration
│   ├── scripts/
│   │   └── document_loader.py       # Document loading utilities
│   ├── chroma_db/                   # ChromaDB storage directory
│   ├── uploads/                     # Uploaded PDF files
│   ├── main.py                      # FastAPI application
│   └── streamlit.py                 # Streamlit demo
├── frontend/
│   ├── src/
│   │   ├── app/
│   │   │   ├── components/
│   │   │   │   ├── chatbox.jsx      # Chat interface
│   │   │   │   ├── pdf_viewer.tsx   # PDF viewer component
│   │   │   │   └── icons/           # UI icons
│   │   │   ├── upload/              # Upload page
│   │   │   ├── rag/                 # RAG interface page
│   │   │   └── demo/                # Demo page
│   │   └── styles/
│   └── package.json
└── README.md
```

## 🔧 API Endpoints

### FastAPI Backend (`http://localhost:8000`)

- `POST /upload/` - Upload a PDF file
- `POST /process/` - Process uploaded PDF and create vector embeddings
- `POST /query/` - Query the document with natural language questions
- `GET /uploads/{filename}` - Access uploaded files

## 🎯 How It Works

1. **Document Upload**: Users upload PDF files through the web interface
2. **Text Extraction**: PDF content is extracted using PyPDFLoader
3. **Text Chunking**: Documents are split into manageable chunks (1500 characters with 200 overlap)
4. **Embedding Generation**: Text chunks are converted to vector embeddings using OpenAI's embedding model
5. **Vector Storage**: Embeddings are stored in ChromaDB with metadata
6. **Query Processing**: User queries are converted to embeddings and matched against stored chunks
7. **Response Generation**: Relevant chunks are retrieved and sent to GPT-4 for answer generation
8. **Streaming Response**: Answers are streamed back to the user in real-time

## 🔑 Environment Variables

Create a `.env` file in the backend directory:

```env
OPENAI_API_KEY=your_openai_api_key_here
```

## 🚨 Troubleshooting

### Common Issues

1. **ChromaDB Collection Errors**: If you encounter collection-related errors, delete the `chroma_db` folder and restart the application
2. **OpenAI API Errors**: Ensure your API key is valid and has sufficient credits
3. **CORS Issues**: The backend is configured to allow requests from `http://localhost:3000`
4. **File Upload Issues**: Ensure the `uploads` directory exists and has proper permissions

### Performance Tips

- For large PDFs, processing may take some time
- ChromaDB collections are persistent - processed documents don't need to be reprocessed
- Use the Streamlit demo for quick testing and development

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🙏 Acknowledgments

- OpenAI for providing the GPT models and embedding API
- LangChain for document processing utilities
- ChromaDB for vector database functionality
- FastAPI and Next.js communities for excellent frameworks