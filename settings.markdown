---
title: Execution Settings
layout: default
---

# Execution Setting

In the following we give an overview of the metrics, workloads and configurations used for the individual subject systems.
In the end we provide, for each subject system, a mapping from setting ID to the triple of configuration, workload and metric. [Jump to mappings](#setting-mapping)

## Metrics and Measurement Tools

The following table provides an overview of the metrics and measurement tools used for our subject systems:

| Project | Measurement Tool | Metric | Unit | 
|---------|-----------------|--------|------|
| MariaDB | BenchBase | Throughput | Requests/s |
| MariaDB | BenchBase | Latency | μs |
| PostgreSQL | BenchBase | Throughput | Requests/s |
| PostgreSQL | BenchBase | Latency | μs |
| x264 | GNU Time | Runtime | s |
| x264 | GNU Time | Peak Memory Usage | kB |
| 7zip | GNU Time | Runtime | s |
| 7zip | GNU Time | Peak Memory Usage | kB |
| brotli | GNU Time | Runtime | s |
| brotli | GNU Time | Peak Memory Usage | kB |
| bzip2 | GNU Time | Runtime | s |
| bzip2 | GNU Time | Peak Memory Usage | kB |
| lrzip | GNU Time | Runtime | s |
| lrzip | GNU Time | Peak Memory Usage | kB |
| xz | GNU Time | Runtime | s |
| xz | GNU Time | Peak Memory Usage | kB |
| FastDownward | GNU Time | Runtime | s |
| FastDownward | GNU Time | Peak Memory Usage | kB |
| Cadical | GNU Time | Runtime | s |
| Cadical | GNU Time | Peak Memory Usage | kB |
| CryptoMiniSAT | GNU Time | Runtime | s |
| CryptoMiniSAT | GNU Time | Peak Memory Usage | kB |
| Dune | GNU Time | Runtime | s |
| Dune | GNU Time | Peak Memory Usage | kB |
| DuckDB | Built-in Benchmark | Runtime | s |
| LibZMQ | GNU Time | Runtime | s |
| LibZMQ | GNU Time | Peak Memory Usage | kB |
| LibZMQ | Built-in Benchmark | Throughput | Mb/s |
| LibZMQ | Built-in Benchmark | Latency | ms |
| LibZMQ | Built-in Benchmark | Trie access time | ns |
| LibZMQ | Built-in Benchmark | Radix tree access time | ns |

## Workloads
For each selected project or domain we give a short description of the selected workloads.

### Compression Domain (7zip, brotli, bzip2, lrzip, xz)

For our compression domain, we used as the workload the compression of the following three corpora:
* `enwik8` -- a 100 MB subset of the English Wikipedia dump. [Link](https://mattmahoney.net/dc/enwik8.zip)
* `silesia` -- a collection of files from the Silesia Corpus. [Link](http://sun.aei.polsl.pl/~sdeor/corpus/silesia.zip)
* `lukas-2d-16-bit` -- A collection of x-ray images of the human body. [Link](https://www.data-compression.info/Corpora/LukasCorpus/index.html)

### SAT Solvers (Cadical, CryptoMiniSAT)
For the SAT solver domain, we used the following three problem instances of the 2024 SAT Solver competition main track:
* `heule-noL-11-12` -- Satisfiable instance from the heule problem family. [Link](https://benchmark-database.de/file/c73edc350cfa8e07af58db50054aea45?context=cnf)
* `mp1-ps-5000` -- Unsatisfiable instance from the popularity-similarity problem family. [Link](https://benchmark-database.de/file/2a53e9c6a25a50d753a94ead66065826?context=cnf)
* `stable-300` -- Satisfiable instance from the argumentation problem family. [Link](https://benchmark-database.de/file/8b31606e10656ff7eb2936262b647443?context=cnf)

### Planning (FastDownward)
We select the following two instances:

* `data-network-opt18-p17` -- Problem 17 from the data-network domain used in the optimal track of the IPC18. [Link](https://github.com/aibasel/downward-benchmarks/tree/master/data-network-opt18-strips)
* `elevators-opt08-p06` -- Problem 6 from the elevators domain used in the optimal track of the IPC 2008. [Link](https://github.com/aibasel/downward-benchmarks/tree/master/elevators-opt08-strips)

### Benchbase-Supported Databases (MariaDB, PostgreSQL)
We use benchbase to benchmark the supported database systems.
We use the provided default configuration files of benchbase, with a duration of 60 seconds for our benchmark.

We use the following workloads for our database systems:
* `TPC-C` -- [Link](https://github.com/cmu-db/benchbase/wiki/TPC-C)
* `TPC-H` -- [Link](https://github.com/cmu-db/benchbase/wiki/TPC-H)
* `auctionmark` -- [Link](https://github.com/cmu-db/benchbase/wiki/AuctionMark)

### DuckDB
For duckdb, we use the in-built benchmark suite to collect the runtime.
We run the following benchmarks:

* `tpch-csv-ingest-lineitem` -- TPC-H based benchmark
* `micro-dict-store-wc-null` -- Microbenchmark that tests wost case performance of stores,
* `micro-create-art-varchar` -- Microbenchmark that tests the performance of creation of indices.

### Message Passing (LibZMQ)
We use the in-built throughput, latency and access time benchmarks of libzmq to collect the metrics.
For latency and throughput we test message sizes from 2^10 to 2^19 bytes, doubling the message size in each step.

* `bench-inproc-lat-{message-size}` -- Latency benchmark with message size of {message-size} bytes.
* `bench-inproc-thr-{message-size}` -- Throughput benchmark with message size of {message-size} bytes.
* `bench-radix-tree` -- Radix tree and trie access time benchmark.

### Video Encoding (x264)
For x264, our workload is the encoding of video files.
We use the following two workloads:

* `aspen-1080p` -- 1080p video of the Aspen tree. [Link](https://media.xiph.org/video/derf/y4m/aspen_1080p.y4m)
* `nocturne-1080p` -- 1080p video of a nocturne. [Link](https://storage.googleapis.com/downloads.webmproject.org/AV2Sequences/420_8bit_1080p/nocturne_aom_sdr_8540-9009_offset2_420_8bit_1080p.y4m)

### Dune (High-Performance Computing)
For Dune, we use a benchmark based on the poisson problem that was suggested to us as a benchmark by a domain expert and is based off a testcase in Dune.
We use two benchmarks executables with different settings:

* `poisson-ug-pk-2d` -- Benchmark that uses a 2-dimensional UGGrid.
* `poisson-non-separated` -- Benchmark that solves the poisson problem with multiple different grids in sequence.

## Configurations
For a subset of our subject systems, we additionally test different configurations.
The following section provides an overview of the configurations used for each subject system.

### Compression Domain (7zip, brotli, bzip2, lrzip, xz)
In the compression domain, we test, in addition to the default setting, the minimum, maximum and mean compression level.

### Dune
For Dune, we configure the binary with three different solvers:
* `CGSolver` -- Conjugate Gradient Solver
* `GradientSolver` -- Gradient Solver
* `LoopSolver` -- Loop Solver

### FastDownward
For FastDownward, we configure the binary with seven different heuristics:

* `lmcut` -- [Landmark Cut heuristic](https://www.fast-downward.org/latest/documentation/search/Evaluator/#landmark-cut_heuristic) (Config ID: 0)
* `hmax` -- [Max heuristic](https://www.fast-downward.org/latest/documentation/search/Evaluator/#max_heuristic) (Config ID: 2)
* `iPDB` -- [Pattern Databases heuristic](https://www.fast-downward.org/latest/documentation/search/Evaluator/#ipdb) (Config ID: 4)
* `lm_zg` -- [Landmark Count heuristic with landmark generation method introduced by Zhu & Givan](https://www.fast-downward.org/latest/documentation/search/LandmarkFactory/#zhugivan_landmarks) (Config ID: 283) 
* `lm_rhw` --  [Landmark Count heuristic with landmark generation method introduced by Richter, Helmert & Westphal](https://www.fast-downward.org/latest/documentation/search/LandmarkFactory/#richterhelmertwestphal_landmarks) (Config ID: 299)
* `lm_hm` [Landmark count heuristic with the landmark generation method introduced by Keyder, Richter & Helmert](https://www.fast-downward.org/latest/documentation/search/LandmarkFactory/#hm_landmarks) (Config ID: 315)
* `lm_exhaust` -- [Landmark count heuristic with exhaustive landmark check](https://www.fast-downward.org/latest/documentation/search/LandmarkFactory/#exhaustive_landmarks) (Config ID: 331)

### x264
For x264, we use, in addition to the default configuration, the following presets:

* `faster` -- Faster preset (Config ID: 1)
* `slower` -- Slower preset (Config ID: 2)

# Setting Mapping

{% for project in site.data.projects %}

## {{ project.name }}

<details>
<summary>Click to show mapping for {{ project.name }} </summary>


{% include {{ project.name | downcase }}/settings.html %}

</details>

{% endfor %}
