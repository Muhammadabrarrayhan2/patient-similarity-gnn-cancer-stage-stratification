# Patient Similarity Graph Neural Network for Cancer Stage Stratification

A graph-based machine learning study for cancer stage stratification using patient similarity networks, lifestyle variables, and clinical features.

## Overview

This repository contains the implementation, paper, and supporting materials for a graph-based cancer stage stratification study. The project investigates whether **patient similarity graph modeling** can improve multi-class cancer stage classification from structured demographic, behavioral, genetic, and treatment-related variables.

Instead of treating each patient as an isolated tabular sample, this work models patients as nodes in a graph and connects them through **k-nearest neighbor similarity**. A **Graph Convolutional Network (GCN)** is then trained on this graph using **PyTorch Geometric**, while **NetworkX** is used for graph construction and visualization. :contentReference[oaicite:2]{index=2}

## Paper Title

**Patient Similarity Graph Neural Network for Cancer Stage Stratification Using Lifestyle and Clinical Variables** :contentReference[oaicite:3]{index=3}

## Abstract

Cancer stage stratification is a clinically meaningful task because stage information directly influences prognosis assessment, treatment planning, and patient management. Most conventional machine learning approaches for structured healthcare data treat patient records as independent tabular samples, which can obscure latent relational patterns among individuals with similar clinical and lifestyle profiles. This study investigates whether patient similarity graph modeling can improve cancer stage classification from heterogeneous patient-level variables. A patient similarity graph is constructed from demographic, behavioral, genetic, and treatment-related features using a k-nearest neighbors strategy, and a two-layer Graph Convolutional Network is applied for multi-class stage prediction. Experimental results show that the graph-based approach is feasible and slightly outperforms a Random Forest baseline, although overall predictive performance remains modest. :contentReference[oaicite:4]{index=4}

## Dataset

The dataset used in this study contains **17,686 patient records** and **16 variables**, including:

- PatientID
- Age
- Gender
- Race/Ethnicity
- BMI
- SmokingStatus
- FamilyHistory
- CancerType
- Stage
- TumorSize
- TreatmentType
- TreatmentResponse
- SurvivalMonths
- Recurrence
- GeneticMarker
- HospitalRegion

The target label is **Stage**, which consists of four classes:

- Stage I: 4471
- Stage II: 4442
- Stage III: 4435
- Stage IV: 4338 :contentReference[oaicite:5]{index=5}

## Methodology

The modeling pipeline consists of the following steps:

1. **Data preprocessing**
   - Remove identifier column (`PatientID`)
   - Encode categorical features using label encoding
   - Handle missing values using most-frequent imputation
   - Standardize features using z-score normalization :contentReference[oaicite:6]{index=6}

2. **Patient similarity graph construction**
   - Represent each patient as a node
   - Construct edges using **k-nearest neighbors**
   - Use **k = 5**
   - Build graph structure with NetworkX :contentReference[oaicite:7]{index=7}

3. **Graph neural network modeling**
   - Use a **two-layer Graph Convolutional Network**
   - Apply ReLU activation and dropout
   - Train with Adam optimizer and cross-entropy loss :contentReference[oaicite:8]{index=8}

4. **Evaluation**
   - Accuracy
   - Weighted F1-score
   - Class-wise precision, recall, and F1-score
   - Confusion matrix :contentReference[oaicite:9]{index=9}

## Main Results

The proposed model was compared against a Random Forest baseline trained on the same preprocessed features.

| Model | Accuracy | Weighted F1-score |
|------|----------:|------------------:|
| Graph Convolutional Network | 0.2606 | 0.2577 |
| Random Forest | 0.2428 | 0.2427 |

The GCN slightly outperformed the conventional baseline, suggesting that **patient similarity graph learning provides useful relational information**, although the overall performance remains modest. :contentReference[oaicite:10]{index=10}

## Class-wise Performance

| Class | Precision | Recall | F1-score | Support |
|------|----------:|-------:|---------:|--------:|
| I   | 0.26 | 0.29 | 0.27 | 894 |
| II  | 0.26 | 0.26 | 0.26 | 889 |
| III | 0.27 | 0.32 | 0.29 | 887 |
| IV  | 0.25 | 0.17 | 0.20 | 868 |

The model performed best on **Stage III** and worst on **Stage IV**, indicating that late-stage patterns were more difficult to separate using the available structured variables. :contentReference[oaicite:11]{index=11}

## Key Takeaways

- Graph-based learning is **feasible** for structured cancer stage prediction.
- Patient similarity graphs can capture local neighborhood structure beyond ordinary tabular classification.
- The current feature space is still **not sufficiently discriminative** for strong stage prediction.
- This project should be viewed as a **rigorous graph-based baseline**, not a clinically deployable diagnostic system. :contentReference[oaicite:12]{index=12}

