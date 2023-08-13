# FAISS





<!---  ![alt text](https://github.com/vvguard/notes/blob/main/image.png?raw=true)  -->

FAISS (Facebook AI Similarity Search) is a Python library developed by Facebook AI Research for efficient similarity search and clustering tasks on large datasets. It's designed to work with high-dimensional data, such as vectors representing images, audio, text embeddings, and more. 

- FAISS is optimized for speed and scalability. Some techniques used to enable fast similarity searches even on massive datasets are
  - index structures
  - quantization
  - multi-threading

- FAISS uses algorithms like cosine similarity, Euclidean distance, inner product, and L2 distance to measure similarity between vectors.

### Indexes
Indexes refer to data structures that are specifically designed to enable efficient similarity search and nearest neighbor retrieval in high-dimensional spaces. FAISS offers various index structures that organize the data in ways that reduce the number of distance calculations needed during similarity search, thereby significantly speeding up the process. 

 - **Flat Index** : This is the simplest type of index. It stores all the vectors in a flat list and allows for exhaustive search, calculating distances to all vectors in the dataset. While not the most efficient, it serves as a baseline for performance comparison.

- **IVF (Inverted File) Index** : This index is based on the idea of inverted files from information retrieval. It divides the dataset into clusters using a coarse quantizer and then creates inverted lists for each cluster. During search, it narrows down the search space to a subset of clusters, significantly reducing the number of comparisons needed.

- **PQ (Product Quantization) Index** : PQ is a compression technique that reduces the dimensionality of vectors and speeds up search. It divides each vector into sub-vectors and quantizes them separately. This allows for efficient storage and computation of distances.

- **HNSW (Hierarchical Navigable Small World) Index** : This index creates a hierarchical graph structure where each node is connected to a small number of other nodes. It constructs a navigable network that helps guide the search process efficiently through the data.

- **L2 Norm Index** : This index optimizes the search process for L2 distance calculations (Euclidean distance). It precomputes norms of vectors, allowing for faster distance calculations. 

- **Inner Product** : This index allows you to retrieve the nearest neighbors based on inner product similarity efficiently. Inner product similarity is a measure of the similarity between two vectors based on the angle between them.
- 
- **Index Composition** : FAISS also provides the ability to combine different index structures to create composite indexes. For example, a combination of an IVF index and a PQ index can leverage the advantages of both structures.

https://gist.github.com/jamescalam/7117aa92235a7f52141ad0654795aa48





