# Secure-Cancellable-Fingerprint-Recognition

## Overview

This repository presents a secure and cancellable fingerprint recognition framework that combines deep feature extraction and random sparse projection-based template protection. The framework generates protected fingerprint templates that preserve verification accuracy while providing revocability, non-invertibility, unlinkability, and resistance to template compromise.

Unlike conventional fingerprint systems that store fixed biometric templates, the proposed approach transforms fingerprint features into cancellable templates that can be revoked and regenerated if compromised.

---

# System Architecture

The complete workflow of the proposed framework is illustrated below:

```text
Fingerprint Image
        │
        ▼
MobileNetV2 Feature Extraction
        │
        ▼
Feature Normalization
        │
        ▼
Random Sparse Linear Mapping (RSLiM)
        │
        ▼
Protected Cancellable Template
        │
        ▼
Enrollment / Template Storage
        │
        ▼
Protected-Domain Matching
        │
        ▼
Euclidean Distance Computation
        │
        ▼
Verification Decision
```

---

# Stage 1: Fingerprint Image Acquisition

The input to the system is a fingerprint image obtained from a fingerprint sensor or benchmark dataset.

The framework has been evaluated on:

* FVC2000
* FVC2002
* FVC2004

Each fingerprint image is resized and preprocessed before feature extraction.

---

# Stage 2: Deep Feature Extraction using MobileNetV2

A pre-trained MobileNetV2 convolutional neural network is used to extract discriminative fingerprint features.

The extracted feature vector contains high-level fingerprint information learned by the deep network.

```text
Input Fingerprint
        │
        ▼
MobileNetV2
        │
        ▼
Feature Vector
```

Advantages:

* Lightweight architecture
* Low computational complexity
* Fast inference
* Strong discriminative representation

---

# Stage 3: Feature Normalization

The extracted feature vector is normalized using Z-score normalization.

```text
x' = (x - μ) / σ
```

where:

* μ = feature mean
* σ = feature standard deviation

Purpose:

* Removes scale differences
* Improves numerical stability
* Ensures uniform feature distribution
* Enhances projection quality

---

# Stage 4: Random Sparse Linear Mapping (RSLiM)

The normalized feature vector is transformed into a cancellable biometric template using Random Sparse Linear Mapping (RSLiM).

A sparse random projection matrix is generated and applied to the normalized feature vector.

```text
Protected Template = Feature Vector × Sparse Projection Matrix
```

RSLiM provides:

* Dimensionality reduction
* Template revocability
* Non-invertibility
* Template diversity
* Unlinkability

Since the projection matrix is random, a compromised template can be replaced simply by generating a new projection matrix.

---

# Stage 5: Cancellable Template Generation

After transformation, the original fingerprint features are never stored.

Only the protected template is retained.

```text
Original Feature
        │
        ▼
RSLiM Transformation
        │
        ▼
Protected Template
```

This template is:

* Revocable
* Non-invertible
* Privacy-preserving

---

# Stage 6: Enrollment Process

During enrollment:

* Fingerprint images are processed through the complete pipeline.
* Protected templates are generated.
* Templates are stored in the database.

Enrollment protocol:

```text
Impression 1
Impression 2
Impression 3
Impression 4
        │
        ▼
Enrollment Templates
```

The first four impressions of each finger are used for enrollment.

---

# Stage 7: Probe Template Generation

During authentication:

* Query fingerprint images are processed using the same pipeline.
* Protected probe templates are generated.

```text
Impression 5
Impression 6
Impression 7
Impression 8
        │
        ▼
Probe Templates
```

The last four impressions are used as probe samples.

---

# Stage 8: Protected-Domain Verification

Verification is performed directly in the protected domain.

The system never compares original fingerprint images.

Instead, it compares protected templates.

```text
Enrollment Template
          │
          ▼
Protected-Domain Matching
          ▲
          │
Probe Template
```

This ensures biometric privacy throughout the verification process.

---

# Stage 9: Euclidean Distance Matching

The similarity between two protected templates is measured using Euclidean distance.

```text
d(x,y) = ||x - y||₂
```

where:

* x = enrollment template
* y = probe template

Interpretation:

* Small distance → same user
* Large distance → different user

Verification decision:

```text
Distance < Threshold
        │
        ├── Accept
        │
        └── Reject
```

---

# Stage 10: Genuine and Impostor Comparisons

Two types of comparisons are generated.

## Genuine Comparisons

Templates belonging to the same finger.

```text
Finger A ↔ Finger A
```

## Impostor Comparisons

Templates belonging to different fingers.

```text
Finger A ↔ Finger B
```

These score distributions are used for performance evaluation.

---

# Stage 11: Performance Evaluation

The framework is evaluated using standard biometric metrics.

## False Acceptance Rate (FAR)

Measures how often impostors are incorrectly accepted.

## False Rejection Rate (FRR)

Measures how often genuine users are incorrectly rejected.

## Equal Error Rate (EER)

The operating point where:

```text
FAR = FRR
```

Lower EER indicates better performance.

## ROC Curve

Plots:

```text
True Positive Rate
        vs
False Positive Rate
```

## Area Under Curve (AUC)

Measures overall verification performance.

Higher AUC indicates better discrimination.

---

# Security Analysis

The framework includes comprehensive security evaluation.

## Revocability Analysis

Evaluates whether new templates can be generated from the same fingerprint using different transformation keys.

## Unlinkability Analysis

Evaluates whether two templates generated from the same fingerprint can be linked.

## Correlation Analysis

Measures statistical relationships between original and transformed templates.

## Brute-Force Attack Analysis

Tests resistance against randomly generated attack templates.

## Reconstruction Attack Analysis

Evaluates whether original fingerprint features can be recovered from protected templates.

---

# Role of Neural Networks (NN1, NN2, NN3)

NN1, NN2, and NN3 are not used for final biometric verification.

Their purpose is only to analyze the separability between:

* Original feature vectors
* Transformed feature vectors

Final authentication is always performed using:

```text
Protected Template
        │
        ▼
Euclidean Distance
        │
        ▼
Verification Decision
```

---

# Key Features

* MobileNetV2-based deep fingerprint representation
* Random Sparse Linear Mapping (RSLiM)
* Cancellable biometric templates
* Protected-domain matching
* Euclidean distance verification
* Revocability
* Unlinkability
* Non-invertibility
* Brute-force resistance
* Reconstruction resistance

---
