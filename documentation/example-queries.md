## Test 1 – Semantic movie search
**User question:**
"Find film om kunstig intelligens og menneskehedens fremtid."

**Expected behavior:**
The system should search the movie database using semantic similarity and return movies that match the meaning of the question.

**Observed behavior:**
The semantic search workflow successfully returned movie results from the Neo4j vector index.

In an earlier test, The Matrix and Interstellar were recommended. The Dark Knight was considered less relevant.

**Evaluation:**
The test demonstrated that semantic search can retrieve movies based on the meaning of a natural language question rather than requiring exact keyword matches.

## Test 2 – Graph-based movie relationships

**User question:**
"Find film, der minder om The Matrix."

**Expected behavior:**
Graph Query should retrieve movies connected to The Matrix through similar themes or shared genres.

**Observed result:**
The graph query returned:

- Inception (2010) – similar theme.
    
- Blade Runner 2049 (2017) – similar theme.
    
- Inception (2010) – shared Science Fiction genre.
    
- Interstellar (2014) – shared Science Fiction genre.
    
- Blade Runner 2049 (2017) – shared Science Fiction genre.

**Evaluation:**
The test demonstrated that Neo4j can retrieve structured relationships between movie nodes.

## Test 3 – AI Agent
**User question:**
"Find film om kunstig intelligens og menneskehedens fremtid, og undersøg hvilke film der minder om hinanden."

**Expected behavior:**
The AI Agent should use Semantic Search to find relevant movies and Graph Query to investigate relationships between them.

**Observed behavior:**
The agent successfully called Semantic Search but did not consistently invoke Graph Query.

Some responses also contained movie titles that were not present in the database.

**Evaluation:**
The test demonstrated that the AI Agent can interpret questions and use semantic search, but it does not yet reliably combine both retrieval tools.

This is a known limitation of the current implementation and an area for future development.