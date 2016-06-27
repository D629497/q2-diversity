---
name: Rarefy, compute pairwise distances, and apply ordination
description: This is a placeholder description for this method.
inputs:
    - feature_table:
        - FeatureTable[Frequency]
        - biom.Table
    - phylogeny:
        - Phylogeny
        - skbio.TreeNode
parameters:
    - metric:
        - Str
        - str
    - depth:
        - Int
        - int
outputs:
    - distance_matrix:
        - DistanceMatrix
        - skbio.DistanceMatrix
    - pcoa_results:
        - PCoAResults
        - skbio.OrdinationResults
---
## Compute PCoA results from a feature table

This workflow rarefies a feature table to an even sampling depth, computes all
pairwise distances using the provided distance metric, and applies principal
coordinate analysis.

### Rarefy feature table

```python
>>> from q2_feature_table import rarefy
>>> rarefied_table = rarefy(feature_table, depth=depth)
```

### Compute pairwise distances

```python
>>> from q2_diversity import beta_diversity
>>> distance_matrix = beta_diversity(metric, rarefied_table, phylogeny=phylogeny)
```

### Apply principal coordinate analysis

```python
>>> import skbio.stats.ordination
>>> pcoa_results = skbio.stats.ordination.pcoa(distance_matrix)
```