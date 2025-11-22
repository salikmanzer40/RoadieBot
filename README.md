# RoadieBot

RoadieBot is a smart chatbot designed to help users with automobile-related questions. It offers troubleshooting advice, maintenance tips, and answers to FAQs for commercial vehicles. Using data from detailed PDF documents, RoadieBot provides accurate and reliable information, making it an essential tool for vehicle owners.

## Features

- 🤖 Intelligent Q&A system powered by Llama 2
- 📚 Knowledge base from PDF documents
- 🔍 Semantic search using FAISS vector database
- 💬 Interactive chat interface via Chainlit
- 🚗 Specialized in commercial vehicle troubleshooting and maintenance

## Prerequisites

- Python 3.8 or higher
- Git

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/salikmanzer40/RoadieBot.git
   cd RoadieBot
   ```

2. **Create a virtual environment (recommended)**
   ```bash
   python -m venv venv
   
   # On Windows
   venv\Scripts\activate
   
   # On Linux/Mac
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Download the Llama 2 Model**
   
   Download the model file `llama-2-7b-chat.ggmlv3.q4_0.bin` from:
   - [Hugging Face - TheBloke/Llama-2-7B-Chat-GGML](https://huggingface.co/TheBloke/Llama-2-7B-Chat-GGML/tree/main)
   
   Place it in the `model/` directory:
   ```
   model/llama-2-7b-chat.ggmlv3.q4_0.bin
   ```

5. **Prepare your PDF documents**
   
   Place your PDF documents in the `data/` directory. These will be used to build the knowledge base.

6. **Create the vector database**
   
   Run the ingestion script to process PDFs and create the vector database:
   ```bash
   python ingest.py
   ```
   
   This will create a FAISS vector store in `vectorstore/db_faiss/`.

## Usage

1. **Start the chatbot**
   ```bash
   chainlit run model.py
   ```

2. **Access the interface**
   
   The chatbot will start and open in your default web browser, typically at `http://localhost:8000`.

3. **Ask questions**
   
   Type your automobile-related questions in the chat interface, and RoadieBot will provide answers based on the knowledge from your PDF documents.

## Project Structure

```
RoadieBot/
├── model.py              # Main chatbot application with Chainlit interface
├── ingest.py             # Script to process PDFs and create vector database
├── requirements.txt      # Python dependencies
├── chainlit.md          # Chainlit welcome screen content
├── LICENSE              # MIT License
├── README.md            # This file
├── data/                # PDF documents directory
│   ├── guide.pdf
│   └── tps.pdf
├── model/               # Model files directory
│   ├── instructions.txt
│   └── llama-2-7b-chat.ggmlv3.q4_0.bin  # (Download separately)
└── vectorstore/         # Generated vector database (created after running ingest.py)
    └── db_faiss/
```

## Configuration

You can modify the following settings in `model.py`:

- **Model path**: Change the model file path in `load_llm()` function
- **Embedding model**: Modify `model_name` in `HuggingFaceEmbeddings` (default: `sentence-transformers/all-MiniLM-L6-v2`)
- **Chunk size**: Adjust `chunk_size` and `chunk_overlap` in `ingest.py` for different text splitting behavior
- **Temperature**: Modify `temperature` in `load_llm()` to control response randomness
- **Max tokens**: Adjust `max_new_tokens` to control response length

## Troubleshooting

- **Model not found**: Ensure the Llama 2 model file is downloaded and placed in the `model/` directory
- **Vector database error**: Run `python ingest.py` to regenerate the vector database
- **Import errors**: Make sure all dependencies are installed: `pip install -r requirements.txt`
- **Memory issues**: The model requires significant RAM. If you encounter memory errors, consider using a smaller model or reducing `max_new_tokens`

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

**Salik Manzer**

## Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/salikmanzer40/RoadieBot/issues).

## Acknowledgments

- [Llama 2](https://ai.meta.com/llama/) by Meta
- [LangChain](https://www.langchain.com/) for the LLM framework
- [Chainlit](https://chainlit.io/) for the chat interface
- [FAISS](https://github.com/facebookresearch/faiss) for vector similarity search
- [Hugging Face](https://huggingface.co/) for embeddings and model hosting
