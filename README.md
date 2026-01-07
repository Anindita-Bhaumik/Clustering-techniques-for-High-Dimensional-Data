# Clustering-techniques-for-High-Dimensional-Data
1. INTRODUCTION
This report presents a comprehensive analysis of clustering techniques applied to a highdimensional dataset containing 9,488 samples and 2,000 features. The aim was to identify
the best clustering method by evaluating performance on both the original data and
reduced-dimensionality data. The techniques which were tried include K-Means, Spectral
Clustering (RBF & NN), Hierarchical Clustering, and Gaussian Mixture Models (GMM). The
Dimensionality Reduction was performed using Principal Component Analysis
(PCA) and Autoencoder before clustering again using the above-mentioned clustering
techniques.
2. DATA OVERVIEW AND PREPROCESSING:
The dataset data.csv consists of 9488 samples and 2000 features, excluding the index.
Standardization was applied using StandardScaler from sklearn to center each feature
around zero with unit variance.
3. CLUSTERING ON ORIGINAL DATA:
The following clustering techniques were applied directly to the raw data:
Method Silhouette Score
K-Means 0.0303
Hierarchical 0.0439
Spectral-NN -0.0049
Spectral-RBF 0.6600
GMM 0.0289
Observations:
➢ Spectral-RBF clustering performed significantly better than all other methods.
➢ Spectral-NN performed poorly, showing a negative silhouette score.
➢ The rest showed low but positive silhouette scores, suggesting weak clustering
structure in high dimensions.
4. DIMENSIONALITY REDUCTION:
Clustering high-dimensional data presents significant challenges such as the curse of
dimensionality, increased noise, and computational complexity. To address these issues,
two dimensionality reduction techniques
1. PCA (linear reduction): PCA was applied after standardizing the data using
StandardScaler and then projected onto the top 10 principal components. These 10
components retained the most variance from the original 2000-dimensional space.
The resulting reduced shape was (9488, 10).
2. Autoencoder (nonlinear): The autoencoder neural network was trained to compress
the 2000-dimensional input into a 10-dimensional latent space; included 3 encoding
and 3 decoding layers using ReLU activations.
3. Activation function used is RELU. The model was trained using reconstruction loss
(MSE) and mini-batch gradient descent(Adam). Once trained, the encoder part was
used to extract the 10-dimensional embeddings. The resulting reduced shape was
(9488, 10).
5. CLUSTERING ON REDUCED DATA (PCA &
AUTOENCODER):
Method PCA Score Autoencoder Score
K-Means 0.0777 0.3124
Hierarchical 0.0494 0.2854
Spectral-NN -0.0041 0.0722
Spectral-RBF 0.3957 0.9234
GMM 0.0719 -0.1126
Observations:
• Autoencoder + Spectral-RBF achieved the highest score (0.9234), outperforming
PCA.
• PCA improved Spectral-RBF (0.7123 vs. 0.6600 on original data).
• Autoencoder significantly boosted K-Means (0.3336 vs. 0.0303).
• GMM performed poorly on reduced data, likely due to Gaussian assumptions.
6. COMPARATIVE ANALYSIS & VISUALIZATION:
➢ Raw data results showed weak clustering structure due to high dimensional noise.
➢ PCA brought slight improvement, but still limited due to its linearity.
➢ Autoencoders, by capturing nonlinear structure, enabled cleaner separability.
➢ Spectral-RBF consistently captured global similarity patterns and benefited greatly
from both PCA and Autoencoder embeddings.
➢ Spectral-NN underperformed likely due to poor neighborhood construction in high
dimensions.
7.CONCLUSION AND RECOMMENDATIONS:
The best clustering result was obtained with:
• Method: Spectral Clustering with RBF kernel
• Embedding: Autoencoder (10 latent dimensions)
• Silhouette Score: 0.8340
