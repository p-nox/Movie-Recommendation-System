# Movie Recommendation System Overview

## Introduction

A Python-based movie recommendation engine using **item-based collaborative filtering** with configurable similarity weighting modes.  
Built with `pandas`, `NumPy`, and `scikit-learn`, this tool predicts movie ratings based on user-item interactions.  
Collaborative filtering is a technique commonly used in recommendation systems, where the system predicts a user's preferences based on the preferences of others.

---

## Table of Contents

1. [Features](#features)  
2. [Requirements](#requirements)  
3. [Getting Started](#getting-started)  
4. [Data](#data)  
5. [Implementation Details](#implementation-details)  
    - [Data Initialization](#data-initialization)  
    - [Similarity Matrix Calculation](#similarity-matrix-calculation)  
    - [Item-Item Collaborative Filtering (Mode 1)](#item-item-collaborative-filtering-mode-1)  
    - [Weighted Prediction (Mode 2)](#weighted-prediction-mode-2)  
    - [User-Count Weighted Prediction (Mode 3)](#user-count-weighted-prediction-mode-3)  
    - [Metrics Calculation](#metrics-calculation)  
6. [Usage](#usage)  
7. [Results](#results)  
8. [Notes](#notes)

---

##  Features

- Reads ratings from CSV file (e.g., `ratings.csv` from [MovieLens](https://grouplens.org/datasets/movielens/))
- Filters out low-activity users and movies for better quality
- Supports three prediction modes:
  - **Simple average** of similar item ratings
  - **Similarity-weighted average**
  - **User-count-weighted similarity**
- Calculates **MAE**, **Precision**, and **Recall** for evaluation
- Efficient computation using pandas + correlation matrices

---

## Requirements

Ensure you have the following Python libraries installed:

- `numpy`: For numerical operations.
- `pandas`: For data manipulation and analysis.
- `scikit-learn`: For machine learning tools.
- `scipy`: For scientific computing functions.

---

## Getting Started

1. Clone the repository to your local machine.
2. Install the required dependencies.
3. Run the main script to see the recommendation system in action.

---

## Data

The recommendation system expects a ratings dataset in CSV format containing:

| userId | movieId | rating |
| ------ | ------- | ------ |
| 1      | 31      | 4.0    |

For this project, the MovieLens dataset was used.( https://grouplens.org/datasets/movielens/latest/)
Only movies and users with at least 5 ratings are retained for better model reliability.

---

## Implementation Details

### * Data Initialization
The `data_init` function reads the movie ratings data, applies preprocessing, and splits it into training and testing sets.

### * Similarity Matrix Calculation
The `calculate_simMatrix` function computes the similarity matrix, allowing the user to choose between Jaccard or adjusted cosine similarity.

### * Item-Item Collaborative Filtering (S1)
The `S1` function performs item-item collaborative filtering. It filters out movies with low predicted ratings, enhancing the relevance of recommendations.

### * User-Item Collaborative Filtering (S2)
The `S2` function combines the filtered results from item-item collaborative filtering with user-item collaborative filtering.

### * Metrics Calculation
The `calculateMetrics` function evaluates the recommendation system's performance using metrics such as Mean Absolute Error (MAE), Precision, and Recall.

---

## Usage
Run the script to train the model, make recommendations, and evaluate performance.The expected command to run the script is as follows:
```python script_name.py <source> <path> <neighbors> <train-percentage>```

   * **source:** Placeholder for the script source file.
   * **path:** Placeholder for the path to the input data file.
   * **neighbors:** Number of neighbors for similarity calculation.
   * **train-percentage:** Percentage of the dataset to be used for training.
     
For example: ```python recommendation_script.py input_data.csv 5 0.8```



## Notes
* Only users and movies with ≥ 5 ratings are retained

* Pearson correlation is used for item similarity

* Ratings are thresholded to binary values (≥3 as positive) for precision/recall 

* For meaningful results, use a dataset with enough density

