# 🌱 Plant Image Classification for Conservation Monitoring

Transfer Learning, Data Augmentation, and Active Learning under Real-World Constraints

## 🔍 Overview

This project explores how computer vision can support conservation monitoring by classifying biologically meaningful plant structures from real-world images. The aim is to model how image-based machine learning systems can enable scalable monitoring of flora across large environments, reducing reliance on manual surveys.

Although focused on plant imagery, the technical challenges and solutions closely mirror those found in biological and diagnostic imaging, including microscopy, where data is noisy, heterogeneous, and costly to annotate.

## 🧰 Tech Stack

- Python
- TensorFlow / Keras
- CNN-based transfer learning
- Generator-based image pipelines
- NumPy, Pandas

## 📊 Dataset

Private dataset – not included in this repository.

Data collection:

- Curated by MSc students as part of a structured data collection exercise
- Images captured using smartphone cameras
- Collected across multiple greenhouses at the Royal Botanic Gardens, Kew

Real-world characteristics:

- Variable lighting
- Inconsistent framing and scale
- Background clutter and occlusion

As a result, this repository focuses on pipeline design, modelling strategy, and evaluation methodology, rather than data distribution.

## 🏷️ Classification Task

The task is formulated as a multi-class image classification problem, with the following plant-structure classes:

- 🏷️ Plant tag
- 🍃 Leaf
- 🌱 Stem
- 🌿 Whole plant
- 🍂 Fruit or leaf

These classes reflect practical conservation scenarios where full plant visibility is not always available and non-biological artefacts (e.g. tags) must be distinguished from plant structures.

## 🛠️ Methodology

### 📦 Data Handling and Pipelines

- Generator-based pipelines were used for:
  - On-the-fly data augmentation via ImageDataGenerator.flow(...)
  - Batched training and evaluation using a custom keras.utils.Sequence DataGenerator

These pipelines enabled memory-efficient loading, scalable batching, and reproducible preprocessing.

Active learning sample selection operated on array-based data pools, with selected samples subsequently passed into generator-backed training loops. Data selection and data loading were handled independently.

### Model Architecture and Transfer Learning

- Implemented a CNN-based image classifier using transfer learning
- A pre-trained CNN backbone was used to leverage generic visual features
- Lower convolutional layers were initially frozen
- Higher layers were fine-tuned to learn plant-structure-specific patterns

Transfer learning was essential due to limited labelled data and high intra-class visual variability.

### 🎨 Data Augmentation

Data augmentation was applied on-the-fly via generator-based pipelines to improve robustness and generalisation, including:

- Random rotations and flips
- Zoom and scale transformations
- Brightness and contrast adjustments

These transformations encouraged the model to learn invariant visual features rather than memorising individual images.

### 🔁 Active Learning Strategy

An active learning approach was explored to assess data efficiency under constrained labelling conditions.

- Training was conducted iteratively rather than in a single pass
- Informative samples were prioritised over random selection
- Particularly useful for analysing visually ambiguous classes (e.g. leaf vs fruit or leaf)

While active learning improved performance relative to naive baselines, it did not outperform transfer learning combined with data augmentation.

## 📈 Training and Evaluation

- Generator-based batching during training and evaluation
- Progressive fine-tuning of the CNN
- Monitoring for overfitting across iterations
- Manual inspection of misclassified images to analyse class ambiguity, lighting effects, and background artefacts

## 🏆 Results

- Baseline accuracy: ~40%
- Active learning peak accuracy: ~60%
- Best-performing configuration: transfer learning combined with systematic data augmentation
- Final accuracy (best model): ~80%

The largest performance gains were achieved through feature reuse via transfer learning and robustness introduced by data augmentation. Active learning provided moderate improvements and insight into data efficiency and class ambiguity.

## 🧫 Relevance Beyond Conservation

The challenges addressed in this project closely resemble those encountered in fluorescence microscopy, diagnostic imaging, and experimental biological datasets, particularly where labelled data is limited and acquisition conditions are noisy.

## ♻️ Reproducibility

- The dataset is private and cannot be shared
- Code is structured to allow substitution of alternative image datasets
- All preprocessing, modelling, and evaluation steps are documented

This mirrors standard practice when working with proprietary or sensitive biological data.

## Summary

This project demonstrates how transfer learning combined with data augmentation can deliver strong performance on noisy, real-world image datasets, while active learning provides additional insight into data efficiency and class ambiguity. The emphasis is on robust pipelines, realistic constraints, and practical applicability to conservation monitoring and biomedical imaging.
