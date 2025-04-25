# Radius-Guided K-Means Clustering

This repository provides a reference implementation of **radius-guided k-means**, a lightweight enhancement to standard k-means clustering. The method improves shape recovery and scalability while preserving interpretability and speed. It relies solely on outputs from standard k-means—cluster centers and point assignments—and adds a simple geometric post-processing step based on cluster radii.

## Related Article

This repository accompanies the article:

*Radius-Guided Post-Processing for K-Means Clustering*  (submitted for review on arXiv)

## Core Idea

After k-means clustering with an intentionally large value of *k*, we compute the **radius** of each cluster (maximum distance of any point to its center), and merge clusters whose radii overlap—i.e., if the sum of radii exceeds the distance between centers.

This corrects:

- Oversegmentation from large *k*

- Poor shape recovery (e.g., rings, moons, non-convex forms) by using oversegmentation as a tool

And it enables:

- Global cluster recovery from local clusters in tiled or distributed clustering scenarios

## Features

- Simple implementation using scikit-learn and NumPy

- Radius-based merging of k-means results

- Support for tiled clustering: scalable, partitioned clustering across spatial or distributed data

- Optional outlier filtering by skipping clusters with radius zero, or only one member

## Contents

- `Radius-Guided Post-Clustering for Shape-Aware, Scalable Refinement of k-Means Results.ipynb` – Core algorithm (KMeansCD class) and demonstration on different datasets (moons, circles, FCPS). Contains all experiments conducted in the paper, and additional experiments.

- `experimental_data/` – CSV files containing clustering performance data from experiments discussed in the paper.

- `data/` – Includes datasets from a third-party source provided under the AGPL v3 license. Please review the accompanying [`data/README.md`](data/README.md) and the [`data/LICENSE.txt`](data/LICENSE.txt) file for detailed licensing information.

## Benchmarks

The method has been tested on:

- Synthetic datasets (e.g., two moons, concentric circles)

- FCPS benchmark suite

- The aforementioned datasets tiled

Across experiments, the method consistently achieved 98–100% median success in noise-free settings with high initial *k*, and performs well under partitioned conditions.

## License

This repository is released under the MIT License with the exception of the data folder. See **Contents** above.
