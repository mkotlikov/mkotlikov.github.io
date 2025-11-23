# Deep Dive: The KotliCluster Algorithm

*Michael Kotlikov - November 23, 2025*

> **TL;DR:** I built KotliCluster as a personal clustering crash course—no stats background, no patience for picking \(K\) or dendrogram cut levels—so I wrote a greedy cosine-based routine that captures arbitrary shapes with minimal configuration.

In the world of data science and machine learning, clustering is a foundational technique for grouping similar data points. Standard algorithms like K-Means and DBSCAN dominate the tooling landscape, yet I often ran into three practical problems: (1) having to guess the number of clusters ahead of time, (2) watching centroid-driven models butcher oddly shaped groups, and (3) DBSCAN flagging "noise" points that simply disappeared instead of being grouped. Hierarchical clustering seemed promising, but picking a linkage and then choosing where to cut the tree felt like another hyperparameter chore I did not understand. With zero formal clustering background, I built KotliCluster as an exercise: dynamic cluster counts, cosine similarity on embeddings, minimal tuning, and the ability to hug arbitrary shapes while forcing every item into some cluster.

## What Is KotliCluster?

KotliCluster is a greedy clustering algorithm that walks through embeddings one by one, assigning each point to the first cluster where it finds a sufficiently similar neighbor (cosine similarity above a threshold). If the algorithm fails to find such a neighbor, the point seeds a brand-new cluster. No K needed, no centroid math, just connectivity.

## Core Logic (Python Pseudocode)

```python
clusters = []

for point in data_points:
    found_cluster = False

    for cluster in clusters:
        for cluster_point in cluster:
            if cosine_similarity(point, cluster_point) >= threshold:
                cluster.append(point)
                found_cluster = True
                break  # stop checking points within this cluster

        if found_cluster:
            break  # stop checking other clusters

    if not found_cluster:
        clusters.append([point])
```

## Key Characteristics

1. **Greedy assignment** – Each point joins the first acceptable cluster; no search for the "best" fit.
2. **Single-linkage connectivity** – Only one sufficiently similar neighbor is required to join a cluster.
3. **No merging step** – Once clusters are separate, they stay separate even if they later intersect.
4. **Order dependence** – Shuffle the input and you may get different clusters.

## Technical Analysis

- **Time complexity** – Worst case, every point compares against all previous points, yielding \(O(N^2)\) similarity checks. Multiply by embedding dimension \(D\) for the full \(O(N^2 \cdot D)\) cost.
- **Space complexity** – Storing \(N\) points of dimension \(D\) gives \(O(N \cdot D)\) memory usage.

## Comparison With Standard Algorithms

| Feature | KotliCluster | K-Means | DBSCAN | Hierarchical (Agglomerative) |
| :--- | :--- | :--- | :--- | :--- |
| Requires \(K\)? | No | Yes | No | No (needs cutoff) |
| Logic | Greedy connectivity | Centroid-based | Density-based | Tree-building |
| Shape | Arbitrary | Spherical | Arbitrary | Arbitrary |
| Noise handling | No (everything clusters) | No | Yes | No |
| Complexity | \(O(N^2)\) | \(O(N \cdot K \cdot I)\) | \(O(N \log N)\)–\(O(N^2)\) | \(O(N^2 \log N)\)–\(O(N^3)\) |
| Determinism | No (order) | No (init) | Mostly | Yes |

### vs. K-Means

K-Means is fast and mathematically grounded when clusters are convex and \(K\) is known. KotliCluster shines when \(K\) is a mystery and shapes are messy duplicates of real embeddings.

### vs. DBSCAN

DBSCAN and KotliCluster both abandon centroids and welcome arbitrary shapes, but DBSCAN distinguishes between core points, border points, and noise. That noise bucket repeatedly hid interesting edge cases in my experiments—points I still wanted grouped—even though they were only a threshold tweak away from belonging. KotliCluster has no noise concept; everything belongs somewhere, for better or worse.

### vs. Hierarchical Clustering

KotliCluster acts like a flat, greedy single-linkage cut. Hierarchical methods build full dendrograms and let you choose linkages and cut heights later, which is powerful once you know what those knobs mean. My criticism—that you still have to pick a level and a linkage and justify both—remains valid for practitioners without a clustering background. KotliCluster skips the tree to stay tiny and direct.

## Potential Improvements

1. **Consensus clustering** – Run KotliCluster multiple times with random orders, then combine results based on co-occurrence frequencies to reduce order sensitivity.
2. **Iterative merging** – After inserting a point, check whether it also bridges another cluster; if so, merge the clusters to avoid fragmentation.
3. **Centroid refinement** – Use KotliCluster for discovery, then execute a single centroid-based pass (e.g., one K-Means iteration) to reassign stragglers.

## Pros & Cons

**Pros**
- Minimal code—roughly 30–40 lines.
- Dynamic cluster counts with intuitive threshold control.
- Handles arbitrary shapes via connectivity.

**Cons**
- Quadratic runtime limits scale to tens of thousands of points.
- Chaining effect can link barely-related points through long similarity ladders.
- Highly order-sensitive and lacks noise rejection.

## Conclusion

KotliCluster scratches an itch I had: "Give me a clustering tool that captures arbitrary shapes, needs almost no configuration, and does not force me to guess \(K\), cut a dendrogram, or accept that 'noise' gets tossed aside." Those complaints are valid—many off-the-shelf methods expose knobs that assume statistical intuition. KotliCluster is a pragmatic, small-scale workhorse for grouping embeddings—perfect for tasks like support-ticket deduping or content clustering. When datasets grow massive or noise handling becomes critical, I still reach for DBSCAN/HDBSCAN, but KotliCluster remains my go-to for fast experiments with unknown landscape.
