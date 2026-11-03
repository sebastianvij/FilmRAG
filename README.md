# FilmRAG – AI-Powered Movie Recommendation System

## 1. Project Overview

FilmRAG is an AI-powered movie recommendation system that combines Retrieval-Augmented Generation (RAG), semantic search and graph-based retrieval.

The purpose of the project is to allow users to search for movies using natural language and explore relationships between movies based on shared themes and genres.

Instead of relying only on keywords, FilmRAG uses vector embeddings to identify movies based on the semantic meaning of a user's question. It also uses a graph database to retrieve structured relationships between movies.

The system is built using n8n, Neo4j Aura and locally hosted AI models through Ollama.

## 2. Technologies

|Technology|Purpose|
|---|---|
|n8n|Workflow automation and AI agent orchestration|
|Neo4j Aura|Graph database and vector search|
|Ollama|Local hosting of language and embedding models|
|Llama 3.2 (3B)|Language model used by the AI agent|
|nomic-embed-text|Embedding model used for semantic search|
|Docker|Running the local n8n instance|

## 3. System Architecture
FilmRAG consists of four main workflows.

### 3.1 Graph Search – Data Ingestion
This workflow imports movie information into Neo4j and generates vector embeddings.

The workflow:
1. Starts through a manual trigger.
    
2. Processes the movie dataset.
    
3. Generates embeddings using `nomic-embed-text`.
    
4. Combines movie information with the generated embeddings.
    
5. Stores the information in Neo4j.
    

### 3.2 Semantic Searc
Semantic Search retrieves movies based on the meaning of the user's question.

The workflow:
1. Receives a natural language question.
    
2. Generates a question embedding using Ollama.
    
3. Searches the Neo4j vector index named `movie_embedding`.
    
4. Retrieves the most relevant movies.
    
5. Uses an LLM to formulate a response based on the search results.


### 3.3 Graph Query
Graph Query uses Cypher queries to explore relationships stored in Neo4j.

It retrieves:
- Movies connected through `SIMILAR_THEME_TO`.
    
- Movies sharing genres through `HAS_GENRE`.

This allows the system to explore relationships that are explicitly represented in the graph database.

### 3.4 AI Agent
The AI Agent is the user-facing component of FilmRAG.

It uses the Llama 3.2 (3B) model through Ollama and has access to two tools:

- Semantic Search
    
- Graph Query
    

The agent is instructed to answer in Danish, use information from the database and avoid inventing movies or relationships.

## 4. Database Structure
The Neo4j database contains two main node types:

- `Movie`
    
- `Genre`

Movie nodes contain properties such as title, year, description and embedding.

The database uses two relationship types:

- `SIMILAR_THEME_TO`
    
- `HAS_GENRE`

### Movie Dataset
The database contains five movies:

|Movie|Year|
|---|---|
|The Matrix|1999|
|Inception|2010|
|Interstellar|2014|
|Blade Runner 2049|2017|
|The Dark Knight|2008|

The dataset includes the genres Science Fiction, Thriller and Action.

### Vector Index
Movie descriptions are converted into 768-dimensional embeddings using `nomic-embed-text`.

The embeddings are stored in Neo4j and searched through a vector index named `movie_embedding`.

## 5. Example Use Cases
FilmRAG supports questions such as:

- "Find movies about artificial intelligence and the future of humanity."
    
- "Which movies have similar themes to The Matrix?"
    
- "Find movies that share genres with Inception."

Semantic Search is used to find movies based on meaning, while Graph Query retrieves explicit relationships between movies.

## 6. Current Limitations
The current implementation has some limitations:

- The movie dataset is relatively small and contains only five movies.
    
- Search results depend on the available movie descriptions and embeddings.
    
- The AI Agent successfully uses Semantic Search but does not consistently invoke Graph Query automatically.
    
- Graph Query works as a separate workflow, but automatic integration of both retrieval methods in a single agent response requires further development.
    
- AI-generated responses may contain incorrect information if the agent does not strictly follow the retrieved database results.

These limitations provide opportunities for further development.

## 7. Project Structure
The project files are organized as follows:

```
FilmRAG/
│
├── README.md
│
├── workflows/
│   ├── FilmRAG-Graph-Search.json
│   ├── FilmRAG-Semantic-Search.json
│   ├── FilmRAG-Graph-Query.json
│   └── FilmRAG-AI-Agent.json
│
├── documentation/
│   ├── agent-configuration.md
│   ├── database-structure.md
│   └── example-queries.md
│
├── screenshots/
│   ├── 01-data-ingestion.png
│   ├── 02-semantic-search.png
│   ├── 03-graph-query.png
│   └── 04-ai-agent.png
│
└── data/
    └── sample-movies.json
```

## 8. Setup and Requirements

To run FilmRAG, the following components are required:

- Docker Desktop
    
- n8n
    
- A Neo4j Aura database
    
- Ollama
    
- `llama3.2:3b`
    
- `nomic-embed-text`
    

### Ollama Models

The required models can be downloaded using:

```
ollama pull llama3.2:3b
ollama pull nomic-embed-text
```

### Configuration

1. Start the n8n instance.
    
2. Configure the Neo4j Aura connection in n8n.
    
3. Configure Ollama so n8n can access the locally hosted models.
    
4. Import the exported workflows from the `workflows` directory.
    
5. Configure the required credentials and workflow connections.
    
6. Execute the data ingestion workflow to populate the database.
    
7. Run the Semantic Search, Graph Query and AI Agent workflows.
    

**Note:** Database credentials and other secrets must be configured locally and must never be included in the exported project files.

## 9. Future Improvements

Potential improvements include:

- Expanding the movie dataset.
    
- Improving the AI Agent's tool selection.
    
- Combining semantic and graph retrieval in a single automated workflow.
    
- Improving response accuracy through stricter grounding in retrieved data.
    
- Adding more movie properties and relationship types.
    

## 10. Conclusion

FilmRAG demonstrates how semantic search, graph databases and locally hosted language models can be combined to create an AI-powered movie recommendation system.

The project provides a foundation for exploring hybrid retrieval methods, where vector search identifies relevant information based on meaning and graph queries retrieve structured relationships.