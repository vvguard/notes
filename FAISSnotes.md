# FAISS





<!---  ![alt text](https://github.com/vvguard/notes/blob/main/image.png?raw=true)  -->

FAISS (Facebook AI Similarity Search) is a Python library developed by Facebook AI Research for efficient similarity search and clustering tasks on large datasets. It's designed to work with high-dimensional data, such as vectors representing images, audio, text embeddings, and more. 




- Efficiency: FAISS is optimized for speed and scalability. Some techniques used to enable fast similarity searches even on massive datasets are
  - Sub index structures
  - Sub quantization
  - Sub multi-threading




- Indexing: FAISS provides different indexing structures like Product Quantization (PQ), Inverted File, Hierarchical Navigable Small World (HNSW), and more. These structures organize the data in a way that speeds up the search process by reducing the number of comparisons needed.

- Vector Similarity: FAISS uses algorithms like cosine similarity, Euclidean distance, inner product, and L2 distance to measure similarity between vectors.

Usage: Users can build and train FAISS indexes on their datasets, and then perform nearest neighbor searches to retrieve items that are similar to a given query. This is particularly useful in scenarios where you want to find similar images, products, or text documents.

Parallelization: FAISS supports multi-threading and GPU acceleration, enabling faster processing and search times.

Integration: While primarily a C++ library, FAISS provides Python bindings to make it accessible and usable within the Python programming environment.

Scalability: FAISS can handle very large datasets efficiently, making it suitable for both research and production-level applications.

Community and Support: FAISS is developed and maintained by Facebook AI Research, so it benefits from ongoing updates and improvements. The library also has an active user community, providing resources and assistance to users.
