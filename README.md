# Label-Efficient Facial Pain Assessment

## Investigating Label Efficiency in Subject-Independent Deep Learning for Facial Pain Classification

This repository contains the research work for an individual research project investigating the relationship between labelled training data and subject-independent performance in deep-learning-based facial pain classification.

## Research Area

**Human Pain Assessment Using Deep Learning**

## Research Question

> How does the amount of labelled training data affect the performance of a deep-learning model for facial pain classification when evaluated on previously unseen subjects?

## Research Gap

Existing research has demonstrated the effectiveness of machine learning and deep learning for automated pain assessment using facial expressions, physiological signals, neural signals, posture and multimodal information.

However, the existing literature primarily focuses on model development, architecture comparison, or predictive performance. There is comparatively less emphasis on systematically investigating how the amount of labelled training data affects generalization to subjects that were not included during training.

This research therefore focuses on the relationship between **labelled-data availability and subject-independent generalization** in facial pain classification.

## Proposed Novelty

The proposed study investigates **label efficiency in subject-independent facial pain classification**.

Rather than focusing primarily on developing a new model architecture, the study will examine how progressively reducing the amount of labelled training data affects the ability of a deep-learning model to classify pain in previously unseen subjects.

The evaluation will maintain a subject-independent experimental protocol and compare performance across different labelled-data conditions.

## Research Objectives

1. Prepare and preprocess a suitable facial pain dataset while maintaining subject-level separation between training and testing data.
2. Develop a deep-learning baseline for facial pain classification.
3. Systematically evaluate model performance using different amounts of labelled training data.
4. Evaluate generalization to subjects that were completely unseen during training.
5. Compare performance using Accuracy, Precision, Recall and F1-score, together with confusion matrices.
6. Analyze how reduced labelled data affects classification performance and generalization.

## Experimental Concept

The study will follow the general pipeline:

```text
Dataset
   ↓
Data Preprocessing
   ↓
Subject-Independent Split
   ↓
Labelled Training-Data Conditions
   ↓
Deep Learning Model
   ↓
Training
   ↓
Evaluation on Unseen Subjects
   ↓
Performance Comparison
