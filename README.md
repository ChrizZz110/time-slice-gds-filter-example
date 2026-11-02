# Time-Slice GDS Filter Example

A demonstration and correctness validation of time-sliced in-memory graph projections using Neo4j Graph Data Science (GDS) `gds.graph.filter`.

## Overview

When building interactive graph analytics applications that evaluate dynamic time windows (such as fraud detection, transaction monitoring, or temporal network analysis), projecting subgraphs directly from the database using Cypher on every query introduces substantial latency and database overhead.

This repository demonstrates the optimized pattern:
1. **Project Broadly Once**: Project a comprehensive in-memory graph with temporal properties (e.g., `occurredAt`, `amount`) stored on the relationships.
2. **Filter Subgraphs in Memory**: Rapidly create temporary time-windowed subgraphs in the GDS catalog using `gds.graph.filter` with parameterized relationship predicates.
3. **Execute Analytics**: Run algorithms (such as PageRank, Centrality, or Community Detection) directly on the sliced graph.
4. **Validate Correctness**: Formally verify that the in-memory filtered subgraph produces the exact same relationship topology as a direct Cypher projection baseline.

---

## Prerequisites

- **Neo4j DBMS**: Neo4j 5.x with the Graph Data Science (GDS) plugin **2.5 or later**.
- **Python**: Python 3.10+ recommended.
- **Jupyter Notebook / JupyterLab** environment.

---

## Getting Started

### 1. Clone and Set Up the Python Environment

Create and activate a virtual environment, then install the required dependencies:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install graphdatascience pandas python-dotenv jupyter
```

### 2. Configure Environment Variables

Copy the example environment file and update it with your Neo4j database credentials:

```bash
cp .env.example .env
```

Edit `.env` to match your database settings:

```dotenv
NEO4J_URI=bolt://localhost:7687
NEO4J_DB=neo4j
NEO4J_USERNAME=neo4j
NEO4J_PASSWORD=your_password_here
```

### 3. Run the Notebook

Start Jupyter and open `time_slice_gds_projections.ipynb`:

```bash
jupyter notebook time_slice_gds_projections.ipynb
```