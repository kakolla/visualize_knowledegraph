# Neo4j Desktop Setup & Visualization

Guide to visualize knowledge graph in Neo4j Desktop

## Installation

1. **Download Neo4j Desktop**
   - Download Neo4j Desktop from  https://neo4j.com/download/

2. **Create new project**
   - Create new project - name it anything

3. **Add Existing Database**
   - Load from .dump file

## Visualizing the Graph

Click Query then connect to database instance, then write
```
:use neo4j-2025-10-20T05-46-11-c7ad3094
```

### See Everything (Warning: slow if >1000 nodes)
```cypher
MATCH (n)-[r]-(d)
RETURN n,r,d
LIMIT 100
```

### By Node Type
```cypher
// All diseases
MATCH (n:Disease)
RETURN n
LIMIT 50

// All proteins
MATCH (n:Protein)
RETURN n
LIMIT 50
```

### With Relationships
```cypher
// Show diseases and what they're connected to
MATCH (d:Disease)-[r]-(other)
RETURN d, r, other
LIMIT 100
```

### Count Nodes by Label
```cypher
MATCH (n)
WHERE NOT n:Document
RETURN labels(n)[0] AS type, count(n) AS count
ORDER BY count DESC
```

### Search for Specific Entity
```cypher
// Find Parkinson's related nodes
MATCH (n)
WHERE n.id =~ '(?i).*parkinson.*'
   OR n.name =~ '(?i).*parkinson.*'
RETURN n
```

### Most Connected Nodes
```cypher
MATCH (n)-[r]-()
WHERE NOT n:Document
RETURN n, count(r) AS connections
ORDER BY connections DESC
LIMIT 20
```
