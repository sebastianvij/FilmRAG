## 1. Overview

The FilmRAG AI Agent is designed to act as a movie recommendation assistant. It receives questions in natural language and uses locally hosted language models through Ollama.

The agent is built in n8n and uses the Llama 3.2 (3B) model.

## 2. Language model

**Model:** llama3.2:3b  
**Platform:** Ollama  
**Purpose:** Understand user questions and generate movie recommendations in Danish.

## 3. Available tools

The agent has access to two workflows as tools.
### Semantic Search

Semantic Search finds movies based on the meaning of the user's question.

It works by:

1. Receiving a natural language question.
    
2. Generating an embedding using nomic-embed-text.
    
3. Searching the movie vector index in Neo4j.
    
4. Returning relevant movie information.

### Graph Query

Graph Query retrieves relationships between movies from Neo4j.

It can identify:

- Movies with similar themes.
    
- Movies connected through shared genres.

The workflow receives a movie title as input and executes a Cypher query against the graph database.

## 4. System instructions

The agent is instructed to:

- Answer in Danish.
    
- Use Semantic Search to find relevant movies.
    
- Use Graph Query to investigate movie relationships.
    
- Only use information returned by the database tools.
    
- Never invent movie titles, genres or relationships.
    
- Explain briefly why a movie is recommended.
    
- Be transparent when the database does not contain relevant information.
    

## 5. Current limitations

During testing, the agent successfully called Semantic Search but did not consistently call Graph Query automatically.

Graph Query was tested separately and returned movie relationships from Neo4j.

Further development is required to ensure that both tools are consistently used together.