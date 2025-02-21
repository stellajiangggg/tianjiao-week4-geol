# Sentinel Altimetry Echo Classification (Week 4 Assignment)

This repository contains code and instructions for classifying **Sentinel altimetry echoes** into **sea ice** vs. **leads** using **unsupervised learning** methods. The goal is to analyze echo waveforms, compute their **average shape** and **standard deviation**, and validate classifications against ESA's official labels using a **confusion matrix**.

#  Table of Contents
- [Overview](#overview)
- [Getting Started](#getting-started)
- [Methodology](#methodology)
- [Results](#results)


---

##  Overview

Satellites like **Sentinel-3** use **radar altimetry** to measure sea surface topography, wind speed, and sea ice distribution. These sensors capture **echo signals** reflected from different surfaces. The signal’s **shape and strength** help distinguish **sea ice from leads**.

🔹 **Objective:** Use **unsupervised clustering** to classify echoes from Sentinel-3 data.  
🔹 **Methods Used:** Gaussian Mixture Models (GMM) for clustering.  
🔹 **Evaluation:** Compare classification results against ESA’s official dataset.  

---

##  Getting Started

The Jupyter Notebook contains the **entire implementation**, including **data preprocessing, clustering, and result visualization**.


 **Materials Needed**

[![🔵](https://img.shields.io/badge/Jupyter-Notebook-blue)](https://cpomucl.github.io/GEOL0069-AI4EO/Chapter1_Unsupervised_Learning_Methods_2.html#)  
📘 **Jupyter Notebook (HTML Version):**  
[View the Jupyter Notebook](https://cpomucl.github.io/GEOL0069-AI4EO/Chapter1_Unsupervised_Learning_Methods_2.html#)  

[![📂](https://img.shields.io/badge/Google-Drive-grey)](https://drive.google.com/drive/folders/1SxmGM9_UJk-M5bEOoTfM_4urvr0257H3)  
📂 **Google Drive Folder (Project Materials):**  
[Access the Google Drive Folder](https://drive.google.com/drive/folders/1SxmGM9_UJk-M5bEOoTfM_4urvr0257H3)  


---

##  Requirements
This project runs best in **Google Colab** but can be executed locally. 

## Methodology
 Steps:
1️⃣ Preprocessing:

Load Sentinel-3 waveform data from NetCDF files.
Remove NaN values and filter signals.
Extract key features: peakiness, standard deviation, echo shape.
2️⃣ Unsupervised Clustering (K-Means & GMM):

K-Means Clustering on Sentinel-2 bands (B2, B3, B4).
GMM clustering applied to altimetry waveform data.
Fit models to extracted features and predict labels.
3️⃣ Evaluation:

Compute mean and standard deviation of classified waveforms.
Compare results with ESA’s classification using a confusion matrix.
## Results
# K-Means Clustering on Sentinel-2 Bands

plt.imshow(labels_image, cmap='viridis')
plt.title('K-means clustering on Sentinel-2 Bands')
plt.colorbar(label='Cluster Label')
plt.show()
Cluster 0: Sea Ice
Cluster 1: Leads

# Gaussian Mixture Model (GMM) Clustering
plt.scatter(X[:, 0], X[:, 1], c=y_gmm, cmap='viridis')
plt.scatter(centers[:, 0], centers[:, 1], c='black', s=200, alpha=0.5)
plt.title('Gaussian Mixture Model')
plt.show()
GMM clusters echoes based on statistical properties.

Mean Echo Plots for Sea Ice and Leads

Sea Ice Echo: Lower amplitude, uniform.
Lead Echo: Higher amplitude, sharp spikes.
Standard Deviation of Echoes

Lead echoes show greater variability than sea ice.
Standard deviation analysis aligns with ESA classification.
Confusion Matrix and Classification Report

from sklearn.metrics import confusion_matrix, classification_report  

conf_m = confusion_matrix(flag_adjusted, clusters_gmm)  
print("Confusion Matrix:\n", conf_m)  

print("\nClassification Report:")  
print(classification_report(flag_adjusted, clusters_gmm))  
Accuracy: Matches ESA’s classification closely.
Misclassifications: Some sea ice regions misclassified due to waveform noise.

