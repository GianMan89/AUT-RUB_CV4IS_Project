# CV4IS Practical Project: Industrial Defect Classification

This repository contains the practical project for **Computer Vision for Industrial Systems (CV4IS)**.

The project can contribute bonus points to the final exam grade. These bonus points are only applied if the exam itself is passed independently.

The project focuses on visual quality inspection using image classification. Given an image of a hazelnut, the goal is to classify whether the object is:

```text
0 = good
1 = defective
````

The project consists of two parts:

1. **Part 1: Core task**
   Train a convolutional neural network (CNN) from scratch for binary defect classification.

2. **Part 2: Additional bonus task**
   Fine-tune a pretrained model for the same task and evaluate its robustness under corrupted image conditions.

Part 1 is the basis of the project and must be completed before Part 2 can be submitted. Part 2 builds on the split, model comparison, and evaluation pipeline from Part 1.

---

## Repository contents

```text
.
├── 01_scratch_cnn_binary_classification_project_skeleton.ipynb
├── 02_transfer_learning_corruption_robustness_project_skeleton.ipynb
├── data/
│   └── .gitkeep
└── README.md
```

The dataset is **not included in this Git repository** to keep the repository small.

---

## Dataset setup

The dataset is provided separately as a zip file.

Run the dataset download/preparation cell in the first notebook. If the automatic download does not work, download the dataset zip manually from Moodle or the provided course link and place it in the `data/` folder.

After extraction, the expected structure is:

```text
data/
  hazelnut_binary_raw/
    good/
    defective/
    metadata.csv
    class_to_label.csv

  hazelnut_binary_corruptions/
    defocus_blur/
      severity_0.50/
      severity_0.75/
    gaussian_noise/
      severity_0.50/
      severity_0.75/
    metadata.csv
    class_to_label.csv
```

The clean dataset is used for the CNN-from-scratch task.
The corrupted dataset is used for the additional bonus task on robustness evaluation.

---

## Part 1: Core task — CNN from scratch

Notebook:

```text
01_scratch_cnn_binary_classification_project_skeleton.ipynb
```

In this part, you train a CNN from scratch for binary classification.

Pretrained models are **not allowed** in Part 1.

You are responsible for:

* creating a reproducible train/validation/test split,
* saving the split as `split.csv`,
* implementing a dataset and dataloaders,
* designing a CNN architecture,
* training and validating the model,
* saving and reloading the final checkpoint,
* evaluating the model with suitable metrics,
* analyzing false positives and false negatives.

The file `split.csv` is important because it records exactly which images were used for training, validation, and testing. It is also reused in Part 2 so that the scratch CNN and fine-tuned model can be compared on the same data split.

The final model checkpoint for Part 1 must be saved as:

```text
model.pt
```

---

## Minimum performance check

The CNN from Part 1 must reach a minimum performance level to receive the corresponding project credit.

The notebook includes a local check on your own test split using:

* defective recall,
* defective F1-score.

These local values help you estimate whether your model is likely to be acceptable.

The official score is computed by the teaching team on a hidden test set. Therefore, your local test score is only an estimate, not the final result.

---

## Part 2: Additional bonus task

Notebook:

```text
02_transfer_learning_corruption_robustness_project_skeleton.ipynb
```

This part can provide additional bonus credit.

Part 2 requires a completed Part 1, because it reuses the same task definition, `split.csv`, and evaluation setup.

In this part, you fine-tune a pretrained computer vision model for the same binary classification task and evaluate its robustness under corrupted image conditions.

The corrupted dataset contains two industrially relevant corruptions:

```text
defocus_blur
gaussian_noise
```

with two severity levels:

```text
0.50
0.75
```

You should compare the fine-tuned model with your scratch CNN and discuss:

* performance on clean images,
* performance under corruptions,
* which corruption causes the largest performance drop,
* how defective recall changes under corruptions,
* what the results imply for industrial deployment.

---

## Report

Your report should explain the main design decisions and results.

For Part 1, discuss:

* dataset split and class distribution,
* CNN architecture,
* training setup,
* loss function and optimizer,
* handling of class imbalance,
* evaluation metrics,
* false positives and false negatives,
* whether the model reached the required performance.

For Part 2, discuss:

* pretrained model choice,
* fine-tuning strategy,
* clean test performance,
* corrupted test performance,
* robustness comparison with the scratch CNN,
* implications for industrial inspection.