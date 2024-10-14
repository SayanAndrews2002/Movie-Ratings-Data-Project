# Movie Ratings Clustering Project

This project focuses on analyzing movie ratings data using matrix factorization techniques and clustering algorithms. The goal is to identify meaningful segments of users and movies, and to evaluate the clustering results through various metrics. We apply both hierarchical and K-means clustering methods on a standardized concatenation of user and movie latent factors.

## Table of Contents
- [Introduction](#introduction)
- [Data](#data)
- [Methodology](#methodology)
  - [Matrix Factorization](#matrix-factorization)
  - [Standardization](#standardization)
  - [Clustering Methods](#clustering-methods)
- [Evaluation Metrics](#evaluation-metrics)
  - [Adjusted Rand Index (ARI)](#adjusted-rand-index-ari)
  - [Silhouette Score](#silhouette-score)
  - [Davies-Bouldin Index](#davies-bouldin-index)
- [Results](#results)
- [Conclusion](#conclusion)
- [Usage](#usage)
- [Acknowledgements](#acknowledgements)

## Introduction
In this project, we explore collaborative filtering and clustering to discover hidden patterns in movie ratings. Using matrix factorization techniques, we decompose the movie-rating matrix into two latent factor matrices, `U` and `V`. These matrices represent user and movie embeddings in a lower-dimensional space. We then standardize these embeddings and apply clustering algorithms to group users and movies based on their latent features.

## Data
The data used in this project comes from a medium-sized matrix (`Rmedium`) containing movie ratings. The dataset consists of:
- **Users**: A subset of users with at least 134 movie ratings.
- **Movies**: A subset of movies included in the original `Rsmall` matrix.

Data is loaded from `ratings_stacked.pkl` and combined with `Rsmall` to form `Rmedium`.

## Methodology

### Matrix Factorization
We use matrix factorization with regularization to compute the latent factors `U` (users) and `V` (movies). These factors are used to represent each user and movie in a lower-dimensional space. The best model is selected based on the evaluation in a previous step.

### Standardization
Before clustering, we standardize the latent matrices `U` and `V` separately to account for arbitrary scaling differences between the user and movie latent spaces. After standardization, the matrices are concatenated into a single matrix, `UVstd`, which is used for clustering.

### Clustering Methods
We apply two clustering techniques:
- **Hierarchical Clustering**: This method builds a tree-like structure of clusters. We use the Agglomerative Clustering algorithm to form 5 clusters.
- **K-means Clustering**: This method partitions the dataset into 5 clusters by minimizing the variance within each cluster.

## Evaluation Metrics
To evaluate and compare the clustering results, we use three metrics:

### Adjusted Rand Index (ARI)
The ARI measures the similarity between two clustering results by considering all pairs of points and checking whether they are assigned to the same or different clusters in each partition. An ARI score of `0.1778` was calculated between hierarchical clustering and the UMAP projection.

### Silhouette Score
This score measures how similar an object is to its own cluster compared to other clusters. A higher Silhouette score indicates better-defined clusters.

### Davies-Bouldin Index
This index is a measure of the average similarity ratio between each cluster and the cluster that is most similar to it. A lower Davies-Bouldin index indicates better separation between clusters.

## Results
The clustering methods provided different insights:
- **Hierarchical clustering** resulted in well-defined clusters in terms of structure, but had less agreement with UMAP projections (ARI of `0.1778`).
- **K-means clustering** also identified clusters, but the structure varied compared to hierarchical methods.

UMAP projections offered a useful visual representation of the latent factors, though consistency with the clustering results was moderate based on the ARI score.

## Conclusion
In this project, we explored clustering on latent space representations of users and movies. The combination of hierarchical clustering and K-means provided a range of insights into the structure of the data. The evaluation metrics, including ARI, Silhouette, and Davies-Bouldin, helped assess the quality and consistency of the clustering.

The ARI score indicates that while UMAP and hierarchical clustering found some overlapping structures, they emphasize different aspects of the data.

## Usage
To run the project, clone the repository and ensure you have the necessary dependencies installed. You can then execute the main script to perform matrix factorization, standardization, clustering, and evaluation.

```bash
git clone https://github.com/yourusername/movie-ratings-clustering.git
cd movie-ratings-clustering
pip install -r requirements.txt
python main.py
