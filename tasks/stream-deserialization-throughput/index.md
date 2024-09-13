A benchmark task measuring the througput of deserializing a grouped RDF stream (that is, a stream in which the elements are either RDF graphs or RDF datasets) from a byte stream to memory.

## Methodology

### Data

Stream distributions of any dataset in the [`stream` category](../../categories/stream/index.md) of RiverBench may be used for this task.

### Workload

The task consists of deserializing RDF data stored in a byte stream to memory in a grouped form (that is, as a stream of RDF graphs or RDF datasets). To isolate the performance of the deserializer itself, the following steps are taken:

- The data (serialized RDF graphs/datasets in the tested serialization format) is preloaded into memory before the benchmark starts.
- The deserialization process is repeated multiple times to amortize the cost of the initial setup, just-in-time code recompilation, and other external factors.
- The deserialized statements are not inserted into any data structure or database, but just temporarily stored in memory and immediately discarded. This is to avoid the overhead of maintaining additional data structures.
    - When possible, the deserialized data should NOT be inserted into a data structure dedicated for RDF graphs or datasets, as these typically include additional processing steps (e.g., updating indexes) that are not part of the deserialization process. Instead, the deserialized statements should ideally be simply iterated over and discarded or inserted into an array.

### Metrics

- **Deserialization throughput (in statements)** – throughput of the deserialization process, measured in RDF statements (triples or quads) per second. This is calculated as the total number of RDF statements deserialized divided by the total time taken to deserialize them.
- **Deserialization throughput (in elements)** – additionally, the throughput may be measured in terms of stream elements (RDF graphs or RDF datasets) per second.

## Results

**See the results for this task reported by the community: [RESULTS](results.md).**

## This task in benchmarks outside of RiverBench

- In the paper about the Jelly streaming protocol, such a benchmark is performed in Section IV.B. The corresponding task in the paper is named "Raw deserialization throughput" and the performance in measured in terms of the number of triples deserialized per second.
    - Sowiński, P., Wasielewska-Michniewska, K., Ganzha, M., & Paprzycki, M. (2022, October). Efficient RDF streaming for the edge-cloud continuum. In 2022 IEEE 8th World Forum on Internet of Things (WF-IoT) (pp. 1-8). IEEE. [https://doi.org/10.1109/WF-IoT54382.2022.10152225](https://doi.org/10.1109/WF-IoT54382.2022.10152225)


## See also

- Version of this task for flat RDF streams: [`flat-deserialization-throughput`](../flat-deserialization-throughput/index.md)
- The inverse task: [`stream-serialization-throughput`](../stream-serialization-throughput/index.md)
