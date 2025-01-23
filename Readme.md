# Knowledge Graph Construction and Expansion with Neo4j

This repository documents my learning journey working with Knowledge Graphs, following the [DeepLearning.AI Knowledge Graphs and RAG course](https://learn.deeplearning.ai/courses/knowledge-graphs-rag/). The project focuses on constructing and expanding a knowledge graph using SEC filings (Form 10-K and Form 13 documents).

## What is a Knowledge Graph?
A Knowledge Graph (KG) is a database that represents data as nodes and edges, where:
- Nodes and edges can have labels
- Both can have properties
- Relationships between data points are explicit and queryable

## Personal Journey & Insights

### Key Discoveries and "Aha!" Moments

#### Vector Integration Breakthrough
After struggling with vector support in Neo4j, I discovered that version 5.16 is the sweet spot for vector operations. The journey involved:
- Initial attempts with v5.13 where vector indexes were introduced but had limitations
- Excitement when finally getting it working: "SUCSSESSSSSSSSSSSSSSSSSS…………. 5.16 VERSION IS IDEAL FOR VECTORS"
- Learning that vector indexes are enterprise-only features

#### Novel RAG Implementation Idea
One of my key insights was developing a unique approach to RAG with knowledge graphs:
1. Use vector search to find relevant chunks
2. Leverage chunk IDs to backtrace relationships
3. Perform complex queries on these relationships
> "...those relationships can be missed from vector search.... my idea."

### Technical Challenges Overcome

#### GenAI Plugin Setup
Found a non-obvious solution for vector functionality:
- Discovered GenAI jar in an unexpected location: `C:\Users\Black Mamba\AppData\Local\Neo4j\Relate\Cache\dbmss....\plugin-resources`
- Learned that copying to the correct plugin folder is crucial
- Realized `dbms.security.procedures.unrestricted=genai.*` wasn't necessary

#### Vector Implementation Learning
Developed a clear understanding of the vector workflow:
1. Create index with node association
2. Specify embedding location
3. Use `db.create.setNodeVectorProperty` for property creation
4. Generate embeddings

### Course Insights (DeepLearning.AI)

#### Critical Lessons
- L5 notebook emerged as the cornerstone for knowledge graph work
  > "L5 NOTEBOOK IS IMPORTANT, ALWAYS CONSULT THAT BEFORE WORKING ON KNOWLEDGE GRAPH"
- Understanding paths and relationships is fundamental
- Direction of relationships affects semantic meaning

#### Data Modeling Revelations
- Converting traditional table structures to graph models requires careful thought
- The power of APOC for data transformation and management
- Importance of proper relationship modeling for semantic accuracy

## Technical Setup

### Neo4j Configuration
1. **APOC Plugin Setup**:
   - Add APOC plugin from Neo4j desktop
   - Configure `neo4j.conf` (located in `.Neo4jdesktop` inside related data, `<database_path>/conf/`):
   ```plaintext
   dbms.security.procedures.unrestricted=apoc.*
   dbms.security.procedures.allowlist=apoc.*
   ```

2. **Important Version Notes**:
   - Neo4j v5.16 is ideal for vector operations
   - Vector support was introduced in v5.13
   - Vector indexes are only supported in enterprise edition
   - With Neo4j v5, APOC is split into Core and Extended editions
     - Core edition: Standard installation
     - Extended edition: Requires manual download from GitHub

### Vector Support Setup
1. **GenAI Plugin**:
   - Location: `C:\Users\Black Mamba\AppData\Local\Neo4j\Relate\Cache\dbmss....\plugin-resources`
   - Copy GenAI jar to the plugin folder (location available in Neo4j desktop app)
   - Required for vector functions to work

### APOC Capabilities
- Data import/export helpers (JSON, CSV)
- Graph algorithms for advanced computations
- Metadata querying (e.g., `apoc.meta.data()`)
- Utility functions (string handling, date calculations)
- Use `CALL apoc.meta.graph()` to visualize schema

## Vector Integration with Neo4j

### Advantages
**Pros:**
- All data in one place
- Embeddings attached to nodes
- Can find and create relationships dynamically
- Enhanced RAG capabilities through relationship backtracing

**Cons:**
- Increased complexity

### Vector Implementation
1. Create an index associated with a node
2. Specify embedding location
3. Create embedding property using `db.create.setNodeVectorProperty`
4. Generate embeddings

## Knowledge Graph Concepts

### Paths
- Paths are matched patterns of nodes and relationships
- Path length = number of relationships in the path
- Can be captured as variables
- Variable length paths allow specifying relationship ranges
- Direction of relationships matters for semantic meaning

### Relationships
- Core component for connecting nodes
- Enable complex querying and pattern matching
- Can be used to trace back connections from vector search results

### Search Capabilities
- Full text indexing available for string matching
- Vector search for semantic similarity
- Combined approaches possible for enhanced retrieval

## RAG with Knowledge Graphs

### Implementation Strategy
1. Find relevant chunks using vector search
2. Use chunk IDs to backtrace relationships
3. Perform complex queries on related data
4. Leverage both semantic similarity and graph structure

### Benefits
- More comprehensive information retrieval
- Captures relationships that might be missed by vector search alone
- Enables complex reasoning through graph traversal

## Scaling Considerations
- Sharding or partitioning data across multiple databases
- Optimization for write-heavy or read-heavy operations
- Performance tuning for large-scale deployments

## Important Notes
- **L5 Notebook**: Critical reference for knowledge graph work
- Always consult L5 before making changes to graph structure
- Converting tables/columns and CSV rows requires careful data modeling
- Consider relationship direction for semantic accuracy

## Future Work and Improvements
- Explore methodologies for vector enhancement of KG
- Develop improved pipelines for data integration
- Investigate advanced scaling solutions
- Implement comprehensive testing strategies

## Resources
- [DeepLearning.AI Course](https://learn.deeplearning.ai/courses/knowledge-graphs-rag/)

- Neo4j Documentation
- APOC Documentation

## Project Structure
- `L3-prep_text_for_RAG.ipynb`: Text preparation for RAG
- `L4-construct_kg_from_text.ipynb`: Initial KG construction
- `L5-add_relationships_to_kg.ipynb`: Critical relationship management
- `L6-expand_the_kg.ipynb`: Graph expansion with Form 13 data

This journey has transformed my understanding of knowledge graphs from simple node-edge structures to powerful tools for complex data relationships and retrieval systems.