# E-commerce Product Recommendation System

This project implements a **machine learning-based product recommendation system** designed to provide personalised product suggestions to users based on their browsing and purchase history. By leveraging various filtering algorithms, the system aims to enhance the overall shopping experience for users and increase sales for e-commerce businesses.

## Problem Statement

The recommendation system addresses several key challenges:
1. Improving the shopping experience by providing relevant product recommendations.
2. Boosting sales by highlighting products that align with user preferences.
3. Tackling the [Cold Start Problem](https://github.com/sarojadhikari076/ecommerce-product-recommendation-system/blob/18d7fb2b8feafd117f7c3f9f859255c2e28cfbe4/cold_start_problem.md) by suggesting products to new users without prior browsing history.

## Dataset

The project utilises an [Amazon Electronics Rating Dataset](https://www.kaggle.com/datasets/vibivij/amazon-electronics-rating-datasetrecommendation/download?datasetVersionNumber=1). Each product and user is assigned a unique identifier to avoid biases. The dataset lacks headers and therefore needs pre-processing before use.

- Download the dataset [here](https://www.kaggle.com/datasets/vibivij/amazon-electronics-rating-datasetrecommendation/download?datasetVersionNumber=1).
- Explore similar datasets from [Amazon Data Repository](https://jmcauley.ucsd.edu/data/amazon/).

## Techniques and Approaches

### 1. Rank-Based Product Recommendation

**Objective**:  
Recommend products with the highest number of ratings and cater to new customers with popular products to address the cold start problem.

**Outputs**:  
Top 5 products with a minimum of 50/100 ratings.

**Approach**:
1. Calculate the average rating for each product.
2. Determine the total number of ratings for each product.
3. Sort products based on average rating and interaction count.
4. Implement a function to fetch the top 'n' products based on a specified interaction threshold.

### 2. Similarity-Based Collaborative Filtering

**Objective**:  
Provide personalised and relevant product recommendations by finding users with similar preferences.

**Outputs**:  
Top 5 product recommendations based on the interactions of similar users.

**Approach**:
1. Convert user IDs to numerical values for ease of computation.
2. Implement a function to find similar users using cosine similarity:
   - Calculate similarity score of a target user with each user in the interaction matrix.
   - Extract and sort the similarity scores, excluding the original user.
3. Create a function to recommend products based on similar user interactions:
   - Identify products with which similar users have interacted but the target user has not.
   - Recommend the specified number of products.

### 3. Model-Based Collaborative Filtering

**Objective**:  
Generate personalised recommendations by analysing past behaviour and preferences, while addressing sparsity and scalability.

**Outputs**:  
Top 5 product recommendations for a specific user.

**Approach**:
1. Convert the product ratings matrix to a **Compressed Sparse Row (CSR)** matrix to reduce memory usage.
2. Apply **Singular Value Decomposition (SVD)** on the sparse matrix, reducing its dimensionality to 50 latent features.
3. Calculate predicted ratings for all users using SVD components.
4. Store predicted ratings in a DataFrame and create a function to recommend products based on rating predictions:
   - Extract and filter unrated products for a user.
   - Sort by predicted ratings in descending order.
   - Recommend top 'n' products.

**Model Evaluation**:
- Compute the Root Mean Squared Error (RMSE) to assess model accuracy.
- Use `mean_squared_error` with `squared=False` to obtain RMSE, which is the square root of the mean of squared errors.

## Project Structure

```bash
.
├── src                           # Source code folder containing implementation scripts
│   ├── rank_based.py             # Script for Rank-Based Recommendations
│   ├── similarity_based.py       # Script for Similarity-Based Collaborative Filtering
│   ├── model_based.py            # Script for Model-Based Collaborative Filtering
│   └── recommendation_system.py  # Main script to run the recommendation system
├── README.md                     # Project Documentation (this file)
└── cold_start_problem.md         # Cold Start Problem Overview

```
