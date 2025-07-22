# AI-Agent-Chat-Files-with-Supabase


<img width="1184" height="838" alt="n8n_ai_agent" src="https://github.com/user-attachments/assets/bafbbfa4-4036-4f41-87c4-3a1b8c3303ba" />

## AI Agent To Chat With Files In Supabase Storage
**Made by [Mark Shcherbakov](https://www.linkedin.com/in/marklowcoding/) from community [5minAI](https://www.skool.com/5minai-2861)**

Manually retrieving and analyzing specific information from large document repositories is time-consuming and inefficient. This workflow automates the process by vectorizing documents and enabling AI-powered interactions, making it easy to query and retrieve context-based information from uploaded files.

The workflow integrates Supabase with an AI-powered chatbot to process, store, and query text and PDF files. The steps include:
- Fetching and comparing files to avoid duplicate processing.
- Handling file downloads and extracting content based on the file type.
- Converting documents into vectorized data for contextual information retrieval.
- Storing and querying vectorized data from a Supabase vector store.

### Set up steps

1. **Fetch File List from Supabase**:
   - Use Supabase to retrieve the stored file list from a specified bucket.
   - Add logic to manage empty folder placeholders returned by Supabase, avoiding incorrect processing.

2. **Compare and Filter Files**:
   - Aggregate the files retrieved from storage and compare them to the existing list in the Supabase `files` table.
   - Exclude duplicates and skip placeholder files to ensure only unprocessed files are handled.

3. **Handle File Downloads**:
   - Download new files using detailed storage configurations for public/private access.
   - Adjust the storage settings and GET requests to match your Supabase setup.

4. **File Type Processing**:
   - Use a Switch node to target specific file types (e.g., PDFs or text files).
   - Employ relevant tools to process the content:
     - For PDFs, extract embedded content.
     - For text files, directly process the text data.

5. **Content Chunking**:
   - Break large text data into smaller chunks using the Text Splitter node.
   - Define chunk size (default: 500 tokens) and overlap to retain necessary context across chunks.

6. **Vector Embedding Creation**:
   - Generate vectorized embeddings for the processed content using OpenAI's embedding tools.
   - Ensure metadata, such as file ID, is included for easy data retrieval.

7. **Store Vectorized Data**:
   - Save the vectorized information into a dedicated Supabase vector store.
   - Use the default schema and table provided by Supabase for seamless setup.

8. **AI Chatbot Integration**:
   - Add a chatbot node to handle user input and retrieve relevant document chunks.
   - Use metadata like file ID for targeted queries, especially when multiple documents are involved.
