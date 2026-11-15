# Label-Efficient Facial Pain Assessment

## Investigating Label Efficiency in Subject-Independent Deep Learning for Facial Pain Classification

This repository contains the research work for an individual research project investigating the relationship between labelled training data and generalization performance in deep-learning-based facial pain classification.

The study uses the SynPAIN dataset to examine how different amounts of labelled training data influence the performance of a baseline deep-learning model.

> **Research status:** Preliminary experiments on SynPAIN have been completed. Evaluation using a second, real-world facial pain dataset and verified subject-independent evaluation remain pending.

---

## Research Area

**Human Pain Assessment Using Deep Learning**

## Research Question

> How does the amount of labelled training data affect the performance of a deep-learning model for facial pain classification when evaluated on previously unseen subjects?

## Research Gap

Existing research has demonstrated the effectiveness of machine learning and deep learning for automated pain assessment using facial expressions, physiological signals, neural signals, posture and multimodal information.

However, existing literature primarily focuses on model development, architecture comparison, or predictive performance. Comparatively less emphasis has been placed on systematically investigating how the amount of labelled training data affects generalization to subjects not included during training.

This research therefore focuses on the relationship between **labelled-data availability and subject-independent generalization** in facial pain classification.

## Proposed Novelty

The proposed study investigates **label efficiency in facial pain classification**.

Rather than focusing primarily on developing a new model architecture, the study examines how progressively reducing the amount of labelled training data affects the ability of a deep-learning model to classify pain.

The intended evaluation uses subject-independent experimental protocols and compares performance across different labelled-data conditions.

---

## Research Objectives

1. Prepare and preprocess a suitable facial pain dataset while maintaining separation between training, validation and testing data.
2. Develop a deep-learning baseline for facial pain classification.
3. Systematically evaluate model performance using different amounts of labelled training data.
4. Investigate generalization to previously unseen subjects.
5. Compare performance using Accuracy, Precision, Recall and F1-score, together with confusion matrices.
6. Analyze how reduced labelled data affects classification performance and generalization.

---

## Dataset

### SynPAIN

The first dataset used in this research is **SynPAIN**, obtained from the Hugging Face dataset repository:

[TaatiTeam/SynPAIN](https://huggingface.co/datasets/TaatiTeam/SynPAIN)

The dataset contains synthetic facial expressions categorized into two classes:

- **Pain**
- **NoPain**

### Dataset Preparation

The preprocessing pipeline included:

- Extraction and preparation of facial images.
- Cropping of the right portrait from the original paired-portrait images.
- Removal of duplicate image crops.
- Organization of images according to their filename identifiers.
- Preparation of training, validation and testing manifests.

After duplicate removal, the prepared dataset contained **5,355 unique image crops**.

| Class | Number of images |
|---|---:|
| Pain | 2,736 |
| NoPain | 2,619 |
| **Total** | **5,355** |

### Dataset Split

The dataset was divided using filename-ID-based grouping.

| Dataset split | Images | Pain | NoPain |
|---|---:|---:|---:|
| Training | 3,748 | 1,942 | 1,806 |
| Validation | 803 | 416 | 387 |
| Testing | 804 | 378 | 426 |
| **Total** | **5,355** | **2,736** | **2,619** |

Overlap verification confirmed zero shared filename IDs across the three splits:

- Training–Validation overlap: 0
- Training–Testing overlap: 0
- Validation–Testing overlap: 0

**Important limitation:** The filename identifiers have not yet been independently verified as actual human subject identifiers. Therefore, the current experiment establishes filename-ID-grouped separation, not confirmed subject-independent evaluation.

---

## Experimental Methodology

### Baseline Model

A lightweight Convolutional Neural Network (CNN), referred to as `SmallCNN`, was implemented as the baseline classifier.

The architecture consists of:

1. Convolutional layer: 3 input channels to 16 feature maps.
2. ReLU activation and max pooling.
3. Convolutional layer: 16 to 32 feature maps.
4. ReLU activation and max pooling.
5. Convolutional layer: 32 to 64 feature maps.
6. ReLU activation and adaptive average pooling.
7. Fully connected classification layer with two output classes.

### Training Configuration

| Parameter | Configuration |
|---|---|
| Framework | PyTorch |
| Model | SmallCNN |
| Input image size | 64 × 64 |
| Optimizer | Adam |
| Learning rate | 0.001 |
| Loss function | CrossEntropyLoss |
| Batch size | 64 |
| Training epochs (controlled experiment) | 8 |
| Random seed | 42 |

### Labelled Training-Data Conditions

The controlled experiment evaluated five training-data fractions:

- 10%
- 25%
- 50%
- 75%
- 100%

Balanced subsets were constructed using nested sampling, with a fixed random seed. This allowed progressively larger subsets to be compared while maintaining a consistent sampling procedure.

The validation and test sets remained unchanged across the different training-data conditions.

---

## Preliminary Experimental Results

The second experiment used eight training epochs and a controlled sampling procedure.

### Test Performance

| Training data | Training images | Test Accuracy | Test F1-score |
|---|---:|---:|---:|
| 10% | 374 | 47.39% | 64.06% |
| 25% | 936 | 52.74% | 66.07% |
| 50% | 1,874 | 57.84% | 65.16% |
| 75% | 2,810 | 61.19% | 52.73% |
| 100% | 3,748 | 68.41% | 64.12% |

### Initial Observations

1. Test accuracy increased as the amount of labelled training data increased, reaching 68.41% with the full training set.
2. The highest test F1-score was observed at the 25% training-data condition (66.07%).
3. F1-score did not increase consistently with additional training data.
4. The 75% condition showed a noticeable reduction in recall and F1-score.
5. The 10% condition achieved high recall (99.74%), but its low accuracy indicates weak class discrimination.

These findings suggest that classification accuracy and F1-score may respond differently to changes in labelled-data availability.

**These results are preliminary.** Each training-data condition has been evaluated in a single controlled run. Repeated-seed experiments, uncertainty estimates and statistical analysis are still required before drawing stronger conclusions.

---

## Current Limitations

The current stage of the research has several limitations:

1. **Synthetic dataset:** The initial experiments use synthetic facial expressions and may not represent the complexity of real-world pain expressions.
2. **Subject verification:** Filename-ID grouping has been performed, but the relationship between filename IDs and actual human subjects remains unverified.
3. **Single experimental run:** Results have not yet been averaged across multiple random seeds.
4. **Limited baseline architecture:** The current experiments use a lightweight CNN rather than a comprehensive comparison of architectures.
5. **Real-world evaluation pending:** Transfer learning and evaluation using a second real-world facial pain dataset have not yet been completed.
6. **Preliminary performance:** The current findings should not be interpreted as evidence of clinical readiness or real-world diagnostic performance.

---

## Future Work

The planned next stages include:

1. Investigating a suitable real-world facial pain dataset, such as the UNBC-McMaster Shoulder Pain Expression Archive, subject to data access and approval.
2. Exploring synthetic-to-real transfer learning by training on SynPAIN and adapting the model using real-world data.
3. Evaluating performance on appropriately held-out real-world subjects.
4. Conducting repeated experiments with multiple random seeds.
5. Generating confusion matrices and further classification analyses.
6. Comparing the baseline model with additional architectures.
7. Investigating the effect of labelled-data availability on synthetic-to-real generalization.

---

## Repository Contents

The repository currently includes:

- `SynPAIN_Training_Pipeline.ipynb` — Jupyter notebook containing the SynPAIN training pipeline and experiments.
- `README.md` — Research overview, methodology, preliminary findings and project status.

Additional experiment outputs, manifests and documentation are maintained in the research project workspace.

---

## Reproducibility

The training pipeline is implemented in Python using PyTorch.

The notebook documents the preprocessing and training workflow used for the initial experiments.

To reproduce the experiments, users will need:

- Python
- PyTorch
- NumPy
- Pandas
- Matplotlib
- Access to the SynPAIN dataset

Dataset files and model weights are not included in this repository.

---

## Research Scope

This is an ongoing individual research project.

The current results represent an initial investigation into label efficiency using synthetic facial pain data. The broader research objective is to understand how labelled-data availability influences generalization, particularly when models are evaluated across different subjects and data domains.

**The conclusions will be updated as further experiments and real-world evaluations are completed.**

---

*Research project: Label-Efficient Facial Pain Assessment*  
*Author: Divya Gupta*
