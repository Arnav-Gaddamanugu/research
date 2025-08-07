# Planar Linkage Truss Analysis Pipeline

This repository contains an end-to-end Python pipeline for kinematic simulation and static force analysis of planar linkage mechanisms. Given a large dataset of planar linkages (from the LINKS repository by Nobari et al.), the code:

1. **Loads linkage definitions** (node coordinates, connectivity, support flags)  
2. **Simulates kinematics** by rotating the driving link through 900 discrete steps  
3. **Assembles a global stiffness matrix** at each pose and applies support constraints  
4. **Solves for nodal displacements and member forces** via sparse LU factorization  
5. **Records force envelopes** (max/min axial force per member) and average displacements  
6. **Outputs a consolidated dataset** of 100 000 linkages with structural annotations  

This design allows high-throughput, reproducible analysis on commodity hardware by processing linkages in configurable batches (default 100 linkages per batch) and serializing intermediate results to disk.

---

## Features

- **Kinematic Solver**  
  Uses Nobari et al.’s open-source LINKS toolkit to compute joint trajectories over 900 steps.

- **Direct-Stiffness Truss Solver**  
  Builds and solves sparse stiffness systems for each static pose in under 0.1 ms.

- **Batch Processing with Dask**  
  Divides a large workload into small, memory-safe batches and parallelizes across cores.

- **Full Dataset Export**  
  Results are saved in a queryable format (HDF5 or Parquet) for downstream analysis and machine-learning workflows.

- **Validation and Reproducibility**  
  Hand-computed four-bar tests (< 1 % error), occasional commercial FEA spot-checks (< 2 % discrepancy), and open-source release under MIT license.

---

## Installation

1. **Clone the repo**  
   ```bash
   git clone https://github.com/Arnav-Gaddamanugu/planar-linkage-truss.git
   cd planar-linkage-truss
