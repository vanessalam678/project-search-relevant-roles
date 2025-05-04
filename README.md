# Job Role Matching

We match the similarity of job roles by generating BERT-based embeddings of each job description and ranking cosine similarity with Memgraph vector search.

- Code: Python
- Dataset (HuggingFace): [job-descriptions](https://huggingface.co/datasets/jacob-hugging-face/job-descriptions)
- Data Handling: [SBERT](https://www.sbert.net/), [Memgraph DB](https://memgraph.com/memgraphdb), [Cypher QL](https://neo4j.com/docs/cypher/)

### Steps:
1. Load dataset from HuggingFace
3. Generate 384-d embedding for each role description using `SentenceTransformers` pretrained model (`paraphrase-MiniLM-L6-v2`)
4. Load job title + embedding pairs into Memgraph using Cypher queries
5. Create Memgraph vector index on the job embeddings
6. Create function `show_relevant_jobs` which takes a query as input, generates its embedding and runs a [vector search](https://memgraph.com/docs/querying/vector-search) for most similar listings by cosine similarity
7. Visualise results with matplotlib

   **Example**: `show_relevant_jobs("SQL, Python, Dashboards, PowerBI")` returns analytics related roles as most relevant:
![image](https://github.com/user-attachments/assets/68349f93-e17e-4565-9ae3-2381d63b8ef7)
