# Wilson++ (Entropy-Aware Spanning Tree Generator)

Wilson++ is a next-generation maze and spanning tree generation algorithm based on a deep generalization of Wilson's algorithm. It introduces entropy-aware random walks, dynamic loop retention, multi-seed initialization, and hierarchical meta-cell refinement. The result is a maze structure that is both organically chaotic and statistically balanced — an emergent harmony between uniformity and structure.

---

## Overview

Classical Wilson’s algorithm generates a uniform spanning tree via loop-erased random walks. Wilson++ extends this process by adding adaptive intelligence and multi-scale refinement to reduce redundancy, improve distribution, and increase aesthetic complexity. It blends stochastic exploration with structural awareness.

Wilson++ can be viewed as a hybrid of Wilson’s algorithm, the Aldous–Broder approach, and multi-level fractal refinement. The result is a high-entropy, low-variance generator suitable for procedural generation, graph sampling, and visualization of emergent connectivity patterns.

---

## Core Features

1. Adaptive Weighted Random Walks:
   Each step of the walk is guided by a probability distribution that depends on local structural cues:
   - in_tree_count: How many of the node’s neighbors are already in the spanning tree.
   - in_walk_count: How many are already in the current walk history.
   - dist_weight: Distance-based bias favoring unexplored frontier regions.
   The resulting weight function:
       weight = (1 / (1 + in_tree_count))^α * (1 / (1 + in_walk_count))^β * (1 + γ * (len(neighs) - in_tree_count))
   where α, β, and γ control the entropy profile of the algorithm.

2. Dynamic Loop Retention:
   Instead of erasing all loops, Wilson++ probabilistically keeps small loops based on neighborhood complexity. This introduces controlled redundancy and gives the maze an organic texture rather than a purely tree-like rigidity.

3. Multi-Seed Initialization:
   Instead of beginning with a single root cell, Wilson++ initializes multiple random seeds proportional to sqrt(N)/4. This parallel growth reduces expected runtime and increases structural diversity by allowing several clusters to merge naturally.

4. Hierarchical Meta-Cell Refinement:
   After generating the initial tree, Wilson++ performs multi-level "meta-cell" refinements. These connect local subregions across increasing scales, creating macro-level connectivity and fractal-like balance.

5. Tunable Parameters:
   α, β, γ → Entropy control for neighbor selection.
   meta_cells, levels → Scale control for multi-level refinement.
   seed → Randomness reproducibility.

---

## Complexity

Classic Wilson’s algorithm has expected O(N log N) time complexity due to long random walks. Wilson++’s multi-seed and entropy-weighted random walks significantly reduce average walk length, approaching practical O(N) runtime for large grids. Hierarchical refinement adds O(N) overhead, keeping total expected complexity near linear.

---

## Conceptual Model

Wilson++ defines a parameterized family of entropy-weighted loop-erased random walks. It interpolates between uniform spanning trees and structured graph growth. Formally, each transition step’s probability is:

    P(next = n) ∝ (1 / (1 + c_tree(n)))^α * (1 / (1 + c_walk(n)))^β * (1 + γ * Δd)

where:
- c_tree(n) = number of neighbors of n already in the tree
- c_walk(n) = number of neighbors of n already in current walk
- Δd = frontier distance factor

This introduces controllable bias while maintaining the spanning tree property.

---

## Installation

Wilson++ is a pure Python implementation. It requires no external libraries.

git clone https://github.com/prabahan/wilson-pp.git
cd wilson-pp
python3 wilson_plus_plus.py  

---

## Usage Example

    from wilson_pp import wilson_pp_advanced, print_maze

    w, h = 20, 12
    maze = wilson_pp_advanced(w, h, seed=42, meta_cells=4, levels=2)
    print_maze(maze, w, h)

---

## Example Parameters

    α = 2.0        # controls resistance to overcrowded nodes
    β = 1.5        # controls resistance to re-entry into the same walk
    γ = 0.5        # controls frontier exploration bias
    meta_cells = 4 # base refinement block size
    levels = 2     # number of refinement passes

---

## Visualization

The included ASCII renderer prints the generated maze in a readable grid format. Cells are connected using “+”, “|”, and “—” patterns, showing the spanning structure. The mazes tend to show both dense clusters and open corridors, reflecting entropy-aware growth.

---

## Theoretical Note

Wilson++ generalizes Wilson’s algorithm by embedding local entropy modulation and hierarchical refinement within loop-erased random walks. It creates a bridge between algorithmic randomness and emergent structure — a new class of entropy-controlled spanning generators.

Mathematically, it can be seen as an entropy-minimized Markov process over grid cells, balancing exploration and consolidation across scales.

---

## Credits

Created by Prabahan (2025)

Wilson++: A Non-Uniform, Entropy-Aware, Hierarchically Refined Generalization of Wilson’s Algorithm.

---

## License

 GPLv3 License. Free to modify and use for research, visualization, or creative works.

---

## Future Directions

- Analyze theoretical uniformity limits as α, β, γ → 0.
- Extend to 3D and higher-dimensional grids.
- Integrate with Tetra Calculus and non-Euclidean metrics.
- Formalize entropy measure for maze complexity.

---

---

Contribution 

Feel free to contribute! Fork the repo, tweak the parameters, improve visualization, or implement new features. All contributions are welcome under GPLv3.


---

Author 

Prabahan 
