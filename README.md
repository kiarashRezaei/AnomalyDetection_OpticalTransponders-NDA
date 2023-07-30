# AnomalyDetection_OpticalTransponders-NDA

## Table of Contents
1. [Problem Definition](#problem-definition)
2. [Datasets](#datasets)
3. [Algorithms](#algorithms)
4. [Data Splitting](#data-splitting)
5. [Cross-validation](#cross-validation)
6. [Principal Component Analysis (PCA)](#principal-component-analysis-pca)
7. [Results](#results)
8. [Comparison](#comparison)
9. [Transfer Learning](#transfer-learning)
10. [Alternative: Covariance Feature Space](#alternative-covariance-feature-space)
11. [Explainable Artificial Intelligence (XAI): GradCAM](#explainable-artificial-intelligence-xai-gradcam)
12. [Conclusion](#conclusion)

## Problem Definition

Lasers in optical transponders can develop faults or be misconfigured, leading to issues such as higher than expected power in the signal and frequency drift in the channel central frequency. These faults can create extra interference for neighboring channels, impacting the overall performance of the optical network. 

The aim of this project is to detect anomalies in optical transponder signals using constellation diagrams, specifically focusing on 16QAM constellations at the receiver of the Channel Under Test (CUT). The task involves identifying normal and faulty classes based on the presence and characteristics of interferers with varying powers and distances from the CUT.

## Datasets
The dataset is sourced from [Constellation Diagrams for Spectrum Anomaly Detection in Optical Networks](https://ieee-dataport.org/open-access/constellation-diagrams-spectrum-anomaly-detection-optical-networks) (F. Musumeci: Network Data Analysis Laboratory). It contains images of the 16QAM constellation at the receiver of the Channel Under Test (CUT), annotated with 5 classes for normal and faulty signal conditions.
Two datasets are used for the project:

1. Full Image Dataset:
   - Constellation diagrams of the 16QAM receiver at the Channel Under Test (CUT).
   - Five classes: 2 normal classes, 3 faulty classes.

2. One-Symbol Image Dataset (from 2 Different Domains):
   - Extracted from full images, focusing on a single symbol in the 16QAM constellation.
   - Enables investigation of localized features and patterns.

## Algorithms

The following algorithms are utilized for anomaly detection:

- One-Class Support Vector Machine (SVM)
- Isolation Forest

## Data Splitting

The datasets are split into training and testing sets for model training and evaluation, respectively.It should be noted the training set contains only normal samples.

## Cross-validation

Cross-validation is performed to assess the model's generalization performance and to avoid overfitting.

## Principal Component Analysis (PCA)

PCA is applied to reduce the dimensionality of the dataset while preserving its important features.

## Results

The performance of the anomaly detection models is evaluated using various metrics, including accuracy, precision, recall, and F1-score.

## Comparison

The results obtained from different algorithms and datasets are compared to determine the most effective approach.

## Transfer Learning

Transfer learning techniques are explored to improve the detection of anomalies in optical transponder signals.
**Approach:**
1- Pure TL: We performed training and hyper parameter tuning on the domain A, evaluated the model on a testset containing images from domain B
2- Domain adaptation:
a) We performed training and hyper parameter tuning on the domain A
b) In each step, the model is re-trained using batches of 10 images from the domain B (16
steps)
c) We evaluate the resulting models on a test set of unseen images belong to domain B

## Alternative: Covariance Feature Space

An alternative approach based on covariance feature space is considered for anomaly detection.
**Approach:**
1- extract statistical features (Mean, Variance, skewness and Kurtosis) of images along the column, in both spatial and Fourier domain.
2- Create a new feature space based on the covariance matrix of each feature vector of each image and check the sparebility of this new feature space
3- PCA
4- Training both models on the covariance feature space (with and without PCA)

## Explainable Artificial Intelligence (XAI): GradCAM

Considering the problem as a classification task, a DNN model is used to classify faulty and normal samples. Then, GradCAM is used to visualize the regions of an image that are important for a its prediction.

## Conclusion

The project concludes with a summary of findings, insights, and potential areas for future research in optical transponder signal anomaly detection.

For more detailed information, refer to the presentation pdf in the repository.
