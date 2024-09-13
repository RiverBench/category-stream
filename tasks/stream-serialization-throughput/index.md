A benchmark task measuring the througput of serializing a grouped RDF stream (that is, a stream in which the elements are either RDF graphs or RDF datasets).

## Methodology

### Data

Stream distributions of any dataset in the [`stream` category](../../categories/stream/index.md) of RiverBench may be used for this task.

### Workload

The task consists of serializing RDF data stored in memory in a grouped form (that is, as a stream of RDF graphs or RDF datasets) to a byte stream. The data is stored in memory in the form of an array of RDF graphs or datasets, or similar. To isolate the performance of the serializer itself, the following steps are taken:

- The data (RDF graphs/datasets) is preloaded into memory before the benchmark starts.
- The RDF data is stored in a data structure that is trivially iterable (e.g., an array of arrays or an array of sets).
- The serialization process is repeated multiple times to amortize the cost of the initial setup, just-in-time code recompilation, and other external factors.
- The serialized data is typically not written to disk, but just temporarily stored in memory and immediately discarded. This is to avoid the overhead of disk I/O.
    - Alternatively, in benchmarks that wish to evaluate the performance of writing to disk, especially considering the impact of different disk usage patterns (e.g., sequential vs. random access), the data may be written to disk.

### Metrics

- **Serialization throughput (in statements)** – throughput of the serialization process, measured in RDF statements (triples or quads) per second. This is calculated as the total number of RDF statements serialized divided by the total time taken to serialize them.
- **Serialization throughput (in elements)** – additionally, the throughput may be measured in terms of stream elements (RDF graphs or RDF datasets) per second.

## Results

**See the results for this task reported by the community: [RESULTS](results.md).**

## This task in benchmarks outside of RiverBench

- In the paper about the Jelly streaming protocol, such a benchmark is performed in Section IV.B. The corresponding task in the paper is named "Raw serialization throughput" and the performance in measured in terms of the number of triples serialized per second.
    - Sowiński, P., Wasielewska-Michniewska, K., Ganzha, M., & Paprzycki, M. (2022, October). Efficient RDF streaming for the edge-cloud continuum. In 2022 IEEE 8th World Forum on Internet of Things (WF-IoT) (pp. 1-8). IEEE. [https://doi.org/10.1109/WF-IoT54382.2022.10152225](https://doi.org/10.1109/WF-IoT54382.2022.10152225)


## See also

- Version of this task for flat RDF streams: [`flat-serialization-throughput`](../flat-serialization-throughput/index.md)
- The inverse task: [`stream-deserialization-throughput`](../stream-deserialization-throughput/index.md)
