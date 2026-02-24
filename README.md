# HLD vs Naive Path Query Benchmark

This project benchmarks two algorithms for maximum-runtime path queries on a workflow dependency graph converted to a tree:

- Naive path query: `O(N)` in the worst case per query
- Heavy-Light Decomposition (HLD) with Segment Tree: `O(log^2 N)` per query

The workflow input is loaded from WfCommons Pegasus JSON format.

## Project Contents

- `hld_vs_naive_benchmark.ipynb`: End-to-end notebook for loading, transforming, benchmarking, and visualization
- `workflow.json`: Input workflow dataset

## What the Notebook Does

1. Loads `workflow.json` using Python `json`.
2. Extracts workflow tasks and maps each task to:
   - `id`
   - `runtime`
   - `parents`
3. Converts DAG dependencies into a strict tree by selecting, for each multi-parent task, the parent with the highest runtime.
4. Implements:
   - Naive max-runtime query from node to root
   - HLD + Segment Tree max-runtime query from node to root
5. Runs a large randomized query benchmark from leaf nodes to root.
6. Reports metrics:
   - Total Time
   - Mean Latency per Query
   - Max Latency per Query
7. Produces three plots:
   - Total execution time bar chart
   - Query latency box plot
   - Path length vs latency scatter plot

## Requirements

Install dependencies in your Python environment:

```bash
pip install numpy pandas matplotlib seaborn pyarrow jupyter
```

## How to Run

1. Open `hld_vs_naive_benchmark.ipynb` in VS Code.
2. Select a Python kernel with the required packages installed.
3. Run all cells in order.

## Expected Output

- Printed benchmark summary table comparing Naive and HLD query performance
- Printed HLD setup/build time (excluded from query timing)
- Three benchmark visualization charts

## Notes

- Query correctness is validated by checking equality of Naive and HLD results across the sampled queries.
- Runtime results depend on hardware, Python version, and workload size.
