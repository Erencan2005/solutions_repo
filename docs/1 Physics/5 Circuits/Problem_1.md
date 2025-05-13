# 🔌 Circuits Problem 1  
## **Equivalent Resistance Using Graph Theory**

---

## 🧠 Motivation

Calculating the equivalent resistance of a complex circuit is essential in circuit analysis. Traditional methods of reducing series and parallel resistors work for small circuits but become cumbersome with larger networks.

Graph theory allows us to represent circuits as graphs:
- **Nodes**: Electrical junctions  
- **Edges**: Resistors (with weights representing resistance)

This method enables a **systematic** and **automated** reduction process, suitable for simulation and optimization.

---

## 🛠️ Option 1: Algorithm Description

We aim to simplify the circuit iteratively using graph-theoretical principles.

---

### 📈 Graph Representation

Given a circuit graph \( G = (V, E) \):

- \( V \): set of nodes (junctions)
- \( E \): set of edges (resistors), each with a weight \( R_e \)

---

### 🔁 Algorithm Overview

1. While the graph has more than two nodes:
    - Identify **series** and **parallel** connections.
    - Replace them with their equivalent resistance.
2. Return the resistance between the source and destination nodes.

---

### ⚙️ Pseudocode

```python
function simplify_circuit(graph, source, target):
    while graph has more than 2 nodes:
        for each node v in graph:
            if v has degree 2 and not in [source, target]:
                # Series reduction
                u, w = neighbors of v
                R1 = resistance(u, v)
                R2 = resistance(v, w)
                R_eq = R1 + R2
                remove v and its edges
                add edge (u, w) with resistance R_eq

        for each pair of nodes (u, v):
            if multiple edges exist between u and v:
                # Parallel reduction
                resistances = [R1, R2, ..., Rn]
                R_eq = 1 / sum(1/R for R in resistances)
                remove all parallel edges
                add edge (u, v) with resistance R_eq

    return resistance between source and target
```

---

### 🧮 Formulas

- **Series**:  
  If resistors \( R_1 \) and \( R_2 \) are in series:  
  $$ R_{\text{eq}} = R_1 + R_2 $$

- **Parallel**:  
  If resistors \( R_1, R_2, ..., R_n \) are in parallel:  
  $$ \frac{1}{R_{\text{eq}}} = \sum_{i=1}^n \frac{1}{R_i} $$

---

## 🧪 Option 2: Python Implementation with `networkx`

```python
import networkx as nx

def equivalent_resistance(graph, source, target):
    G = graph.copy()
    while True:
        changed = False

        # Series reduction
        for node in list(G.nodes):
            if node in [source, target] or G.degree[node] != 2:
                continue
            neighbors = list(G.neighbors(node))
            if len(neighbors) != 2:
                continue
            u, v = neighbors
            if G.number_of_edges(u, node) > 1 or G.number_of_edges(v, node) > 1:
                continue

            R1 = G[u][node]['resistance']
            R2 = G[v][node]['resistance']
            R_eq = R1 + R2

            G.add_edge(u, v, resistance=R_eq)
            G.remove_node(node)
            changed = True
            break

        if changed:
            continue

        # Parallel reduction
        for u, v in list(G.edges()):
            parallel_edges = [(u, v)]
            if G.number_of_edges(u, v) > 1:
                resistances = [G[u][v]['resistance']]
                for i in range(G.number_of_edges(u, v) - 1):
                    resistances.append(G[u][v + f'_{i}']['resistance'])
                R_eq = 1 / sum(1 / R for R in resistances)
                G.remove_edges_from(parallel_edges)
                G.add_edge(u, v, resistance=R_eq)
                changed = True
                break

        if not changed:
            break

    return G[source][target]['resistance']
```
![alt text](image-1.png)
---

## 🔬 Examples

### Example 1: Series

- Nodes: A — B — C
- Resistors:  
  - A-B: 2 Ω  
  - B-C: 3 Ω

**Expected Result**:  
$$ R_{\text{eq}} = 2 + 3 = 5 \, \Omega $$

---

### Example 2: Parallel

- Nodes: A, B
- Resistors:  
  - A-B: 4 Ω  
  - A-B: 6 Ω

**Expected Result**:  
$$ \frac{1}{R_{\text{eq}}} = \frac{1}{4} + \frac{1}{6} = \frac{5}{12} \Rightarrow R_{\text{eq}} = \frac{12}{5} = 2.4 \, \Omega $$

---

### Example 3: Nested

- A—B—C with 3 edges from A to C (parallel to path A-B-C)
  - A-B: 1 Ω  
  - B-C: 1 Ω  
  - A-C: 2 Ω

- Series path A-B-C: \( 1 + 1 = 2 \, \Omega \)  
- Parallel with direct A-C:  
  $$ \frac{1}{R_{\text{eq}}} = \frac{1}{2} + \frac{1}{2} = 1 \Rightarrow R_{\text{eq}} = 1 \, \Omega $$

---

## 🧠 Analysis

- **Time complexity**:  
  - Worst-case: \( O(n^2) \) for checking all node pairs for parallel edges.
  - More efficient with union-find or disjoint set optimizations.

- **Improvements**:  
  - Use DFS or BFS to identify reducible structures.
  - Apply symbolic computation for variable resistors.

---

## ✅ Conclusion

Graph-based reduction provides a robust way to compute equivalent resistance for any circuit topology. This method can be used in simulation tools, CAD software, and optimization applications.

