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

Quantization, in the context of FAISS (Facebook AI Similarity Search), refers to a technique used to compress and represent high-dimensional vectors in a more compact form. This technique is particularly valuable when dealing with large datasets containing vectors with many dimensions, such as image embeddings, audio features, or text representations.

The main idea behind quantization in FAISS is to reduce the memory and computational requirements associated with storing and processing high-dimensional vectors while preserving the essential characteristics that enable effective similarity search. Here's how quantization works in FAISS:

1. **Vector Quantization**: In a high-dimensional space, vectors might have similar patterns or directions even though they're not exactly the same. Vector quantization groups these similar vectors into clusters, where each cluster is represented by a centroid vector. Instead of storing all the original vectors, you store the centroids of these clusters, significantly reducing the memory footprint.

2. **Product Quantization (PQ)**: One of the quantization techniques used in FAISS is called Product Quantization. In PQ, a high-dimensional vector is divided into multiple sub-vectors. Each sub-vector is quantized separately, and the quantized sub-vectors are combined to form a quantized representation of the original vector. This reduces the complexity of quantization and improves the efficiency of search operations.

3. **Search Efficiency**: Quantization allows FAISS to perform similarity searches more efficiently. Instead of comparing the original high-dimensional vectors, FAISS compares the quantized vectors. This can greatly reduce the number of distance calculations needed during search operations.

4. **Trade-off**: Quantization involves a trade-off between accuracy and compression. While quantization reduces the memory and computation required, it may introduce some loss of precision due to the nature of grouping similar vectors.

In summary, quantization in FAISS is a technique that involves compressing high-dimensional vectors by grouping them into clusters and representing those clusters with centroids. This makes it possible to efficiently store and search through large datasets of high-dimensional vectors while reducing memory and computational requirements. Product Quantization (PQ) is a specific quantization technique used in FAISS to achieve these benefits.









In FAISS (Facebook AI Similarity Search), partitioning refers to the process of dividing a large dataset of vectors into smaller, manageable subsets called partitions or clusters. Partitioning is a key component in building index structures that enable efficient similarity search and retrieval of nearest neighbors.

Partitioning serves two main purposes in FAISS:

1. **Improved Efficiency**: When dealing with a massive dataset, performing exhaustive searches to find the nearest neighbors of a query vector can be computationally expensive. By partitioning the dataset, FAISS can restrict the search space to a subset of vectors that are likely to contain the nearest neighbors. This reduces the number of distance calculations needed during search operations and speeds up the process.

2. **Optimized Indexing**: Partitioning plays a significant role in the design of index structures. Many index types, such as inverted file indexes (IVF) and hierarchical navigable small world indexes (HNSW), rely on partitioning to organize the data efficiently. Each partition or cluster corresponds to a subset of the data that can be processed and searched independently.

Here's how partitioning works in FAISS:

1. **IVF (Inverted File) Index**: In IVF, partitioning involves dividing the dataset into clusters using a coarse quantizer. Each cluster corresponds to an inverted list that contains pointers to the vectors in that cluster. During search, the index can quickly identify which clusters are likely to contain the nearest neighbors and perform more refined searches within those clusters.

2. **HNSW (Hierarchical Navigable Small World) Index**: HNSW creates a hierarchical graph structure where each node represents a vector. The graph is divided into layers, and each layer contains vectors that are closer in distance to each other. This hierarchical partitioning guides the search process, allowing for efficient nearest neighbor retrieval.

3. **Composite Indexes**: Partitioning can also be used in combination with other index structures to create composite indexes. These indexes leverage the advantages of different partitioning and indexing techniques to further enhance search efficiency.

In summary, partitioning in FAISS involves dividing a large dataset of vectors into smaller subsets to improve the efficiency of similarity search operations. It's a fundamental concept in the construction of index structures that optimize search times and enable fast retrieval of nearest neighbors.




Partitioning and vector quantization are related concepts in FAISS, but they are not exactly the same. Both concepts are used to optimize the efficiency of similarity search operations, but they serve slightly different purposes and are applied in different contexts.

1. **Vector Quantization**:
   - Vector quantization involves grouping similar vectors together and representing them by a single representative vector, often referred to as a centroid.
   - The purpose of vector quantization is to compress the dataset by reducing the number of unique vectors stored, while retaining the essential characteristics of the data.
   - This compression is achieved by quantizing vectors into clusters, which are then represented by the centroids of those clusters.
   - The Product Quantization (PQ) technique in FAISS is an example of vector quantization. It divides vectors into sub-vectors and quantizes each sub-vector separately to create compact representations.

2. **Partitioning**:
   - Partitioning involves dividing a dataset into smaller subsets or partitions, where each partition contains a group of vectors.
   - The primary purpose of partitioning is to improve the efficiency of search operations by narrowing down the search space.
   - Partitioning is often used in the context of index structures. Different types of indexes use partitioning to organize and manage the data for efficient similarity search.
   - For example, the Inverted File (IVF) index in FAISS divides the dataset into clusters (partitions), where each cluster has an associated inverted list of vectors. This partitioning allows for faster search by targeting relevant clusters during search operations.

While both vector quantization and partitioning contribute to optimizing similarity search in FAISS, they are used at different stages and serve slightly different goals. Vector quantization primarily focuses on compressing data by representing clusters of similar vectors with centroids. Partitioning, on the other hand, aims to enhance search efficiency by organizing the data into manageable subsets within the context of index structures.





In FAISS, the `IndexIVFPQ` class is used to create an index structure based on the Inverted File with Product Quantization (IVFPQ) technique. This index is particularly useful for efficient similarity search in high-dimensional spaces using quantization and inverted file structures. When initializing an instance of `IndexIVFPQ`, you need to provide several parameters to configure its behavior. Here are the parameters you can specify:

1. **d**: (int) The dimensionality of the vectors you'll be indexing.

2. **nlist**: (int) The number of inverted lists or clusters to create. This parameter controls the granularity of partitioning your dataset.

3. **m**: (int) The number of centroids to use for each sub-quantizer in the Product Quantization part. Larger values may lead to better accuracy but require more memory and computational resources.

4. **nbits**: (int) The number of bits for encoding each sub-quantizer's index. A higher value may provide better accuracy but consumes more memory.

5. **train_on_gpu**: (bool) Whether to perform training on GPU. Training is used to learn the centroids in the PQ stage. Enabling this can speed up the training process if you have a GPU available.

6. **use_float16**: (bool) Whether to use 16-bit floating-point representation for quantized vectors. This can reduce memory usage but might impact accuracy.

7. **quantizer**: (faiss.Index) The quantizer index to be used for assigning vectors to inverted lists. This can be an instance of another index type, like `IndexFlatL2` or `IndexHNSW`.

8. **use_precomputed_table**: (bool) Whether to use precomputed codes for searching. Enabling this can speed up the search process but requires additional memory.

9. **indexes_options**: (str) Options for the sub-indexes used in the IVFPQ structure. This can include settings like 'PQ32' or 'PQ64' to define the sub-quantizer's behavior.

These parameters collectively define how the `IndexIVFPQ` index will be constructed, how quantization and partitioning will be performed, and how searches will be executed. It's important to choose appropriate values based on the characteristics of your data, your computational resources, and your desired balance between search accuracy and speed.

Remember that this is a high-level overview of the parameters, and it's always a good idea to refer to the official FAISS documentation for the most up-to-date and detailed information on using `IndexIVFPQ`.


-------------------------------------------------------------------------------------------------------------------

In FAISS, the `IndexIVFFlat` class is used to create an index structure based on the Inverted File with Flat (IVFFlat) technique. This index is useful for efficient similarity search and retrieval of nearest neighbors in high-dimensional spaces using an inverted file structure. When initializing an instance of `IndexIVFFlat`, you need to provide several parameters to configure its behavior. Here are the parameters you can specify:

1. **d**: (int) The dimensionality of the vectors you'll be indexing.

2. **nlist**: (int) The number of inverted lists or clusters to create. This parameter controls the granularity of partitioning your dataset.

3. **quantizer**: (faiss.Index) The quantizer index to be used for assigning vectors to inverted lists. This can be an instance of another index type, like `IndexFlatL2` or `IndexHNSW`.

4. **metric_type**: (int) The metric type to be used for distance calculations. This parameter determines the distance function used to compare vectors. Common values include `faiss.METRIC_L2` for Euclidean distance and `faiss.METRIC_INNER_PRODUCT` for inner product similarity.

5. **shard_type**: (int) The shard type to be used. This parameter affects how data is distributed across devices in a multi-GPU setup. Common values include `faiss.IO_32_BITS` and `faiss.IO_64_BITS`.

6. **shard_threshold**: (int) The threshold for partitioning the data across devices. Vectors with IDs below this threshold will be assigned to one device, and vectors with IDs equal to or above this threshold will be assigned to another device in a multi-GPU setup.

7. **shard_bits**: (int) The number of bits to use for data partitioning across devices in a multi-GPU setup.

8. **use_float16**: (bool) Whether to use 16-bit floating-point representation for vectors in the index. This can reduce memory usage but might impact accuracy.

9. **index**: (faiss.Index) The index to be used within each inverted list. This can be an instance of another index type, like `IndexFlatL2` or `IndexHNSW`.

These parameters collectively define how the `IndexIVFFlat` index will be constructed, how data will be partitioned and quantized, and how similarity search operations will be performed. The choice of parameters should be based on the characteristics of your data, your computational resources, and your desired balance between search accuracy and speed.

Keep in mind that this is a high-level overview of the parameters, and you should refer to the official FAISS documentation for the most up-to-date and detailed information on using `IndexIVFFlat`.
