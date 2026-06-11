# MIXER: Multimodal Instagram Engagement Prediction

This repository contains the code and experimental material for the paper:

**Explaining Feature Contributions in Multimodal Instagram Engagement Prediction**

The project studies Instagram engagement prediction using multimodal post-level information, including caption text, image content, and metadata. The goal is not to optimize for deployment or marketing use, but to provide a transparent and reproducible empirical analysis of how different modalities and feature groups contribute to engagement prediction.

## Overview

We model Instagram engagement as a supervised classification task based on engagement rate. For each post, engagement rate is computed from likes and comments normalized by the number of followers. The target is then discretized at different levels of granularity:

- binary classification;
- three-class classification;
- five-class classification.

The experiments compare unimodal and multimodal configurations across three representation families:

- **traditional representations**, based on TF-IDF caption features, handcrafted image descriptors, and metadata;
- **semantic representations**, based on SBERT text embeddings, EfficientNet-B0 image embeddings, and metadata;
- **vision-language representations**, based on CLIP text and image embeddings, combined with metadata.

The best-performing multimodal configuration is then analyzed with post-hoc explainability methods to inspect modality-level and feature-group-level contributions.



## Data

The experiments are based on the public [Instagram Influencers Dataset](https://sites.google.com/site/sbkimcv/dataset/instagram-influencer-dataset) The repository does not redistribute raw Instagram data unless permitted by the original dataset license and access conditions.

Users should obtain the dataset from the original source and place the required files in the appropriate data directory. Any preprocessing scripts assume that the input files follow the expected structure described in the code or accompanying documentation.

## Target Definition

For each post, engagement rate is defined as:

ER = 100 * (likes + comments) / followers

The engagement rate is log-transformed to reduce the effect of the strongly right-skewed distribution. Classification labels are then obtained through quantile-based discretization.

## Experimental Setting

The experiments use a chronological split:

- training posts: January 2017 - October 2018;
- validation posts: November 2018;
- test posts: December 2018.

Training data are balanced by creator category at the account level. Validation and test data preserve the natural distribution.


## Models

The repository includes experiments with the following classifiers:

- Linear Support Vector Machine;
- Gaussian Naive Bayes;
- Random Forest;
- XGBoost.

Hyperparameter tuning is intentionally limited to the parameters required for model selection. This keeps the comparison bounded and reproducible under a fixed computational budget.

## Explainability

The explainability analysis focuses on the strongest multimodal configuration. It includes:

- global SHAP-based feature attributions;
- modality-level contribution analysis;
- metadata feature-group analysis;
- local perturbation-based image explanations.

The explainability results are used to inspect which modalities and feature groups contribute most to engagement prediction across different target granularities.

## Reproducibility Notes

To reproduce the experiments:

1. obtain the dataset from the original source;
2. place the required files in the expected data directory;
3. install the required Python dependencies;
4. run the preprocessing scripts;
5. generate text, image, and metadata representations;
6. train and evaluate the models;
7. run the explainability scripts on the selected configuration.

Example commands will depend on the released code structure.

## Citation

If you use this repository, please cite the associated paper:

```bibtex
@inproceedings{mixer2026,
  title     = {Explaining Feature Contributions in Multimodal Instagram Engagement Prediction},
  author    = {Anonymous},
  booktitle = {},
  year      = {2026}
}
```
The citation will be updated after publication.

