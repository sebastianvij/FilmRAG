## 1. Database

FilmRAG uses Neo4j Aura as its graph database and vector database.

The database stores movie information, genre information, relationships and vector embeddings.

## 2. Node types

### Movie

Each movie node contains:

- `title`: Movie title.
    
- `year`: Release year.
    
- `description`: Short movie description.
    
- `embedding`: Vector representation of the movie description.
    

### Genre

Genre nodes represent movie categories and contain:

- `name`: Genre name.
## 3. Relationships

The database uses two main relationship types.

### SIMILAR_THEME_TO

Connects movies that share similar themes.

### HAS_GENRE

Connects movies to their genres. The same genre can connect multiple movies indirectly through the genre node.

## 4. Movie dataset

The database contains five movies:

|Movie|Year|
|---|---|
|The Matrix|1999|
|Inception|2010|
|Interstellar|2014|
|Blade Runner 2049|2017|
|The Dark Knight|2008|

The database contains the genres Science Fiction, Thriller and Action.

## 5. Vector search

Movie descriptions are converted into numerical embeddings using the `nomic-embed-text` model.

The embeddings are stored in Neo4j and searched using a vector index named `movie_embedding`.

The vector index uses 768-dimensional embeddings.

## 6. Data ingestion

The data ingestion workflow performs the following operations:

1. Starts through a manual trigger.
    
2. Sends movie data to Neo4j.
    
3. Splits the movie data into individual records.
    
4. Generates embeddings using Ollama.
    
5. Combines movie information and embeddings.
    
6. Saves the embeddings in Neo4j.

This makes the movie collection available for semantic retrieval.