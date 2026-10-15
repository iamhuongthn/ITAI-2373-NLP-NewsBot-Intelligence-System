
# NewsBot Evaluation Documentation

## Overview

This directory stores the evaluation evidence for the NewsBot Intelligence System.

The goal is to separate measured results from demonstration examples and manually reviewed predictions.

## Evaluation Files

### newsbot_ner_manual_review.csv

Contains a reproducible sample of 30 spaCy named entity predictions.

Each prediction includes:

- Article identifier
- News category
- Extracted entity
- Predicted entity type
- Character offsets
- Article context
- Span correctness
- Label correctness
- Corrected entity type
- Error category
- Reviewer notes

The `correct_span` and `correct_label` columns use `yes` or `no`.

Manual evaluation is complete only when all 30 predictions have been reviewed.

### newsbot_testing_results.csv

Contains the results of the NewsBot end-to-end demonstration.

Includes predicted categories, confidence estimates, sentiment labels, entity counts and execution status.

Synthetic examples and external-source tests must be identified separately.

### model_comparison.csv

Contains classification metrics for the compared model configurations.

Recommended columns:

- Model
- Test Accuracy
- Macro Precision
- Macro Recall
- Macro F1
- Cross-Validation Mean
- Cross-Validation Standard Deviation

Only include this CSV after exporting the actual results from the notebook.

## Evaluation Methodology

### Classification

The BBC dataset uses a stratified 80/20 train/test split.

Five-fold cross-validation is performed on the training portion, with preprocessing fitted separately inside each fold.

The primary model-selection metric is macro F1.

The held-out test set is used for final evaluation.

### Named Entity Recognition

Manual review examines predicted entity spans and labels.

Agreement is calculated from the completed annotations.

Because the sample contains predicted entities rather than fully annotated articles, this review does not establish full NER precision, recall or F1.

### External Article Testing

External-source articles are processed using the trained NewsBot pipeline.

Their expected categories are manually assigned to the five BBC categories.

Results from a small number of external articles are exploratory and should not be presented as a reliable generalization-accuracy estimate.

## Reproducibility

The completed NER review CSV should be stored in this directory.

The notebook should load the completed file for evaluation without requiring the instructor to annotate the entities again.

The interactive review interface is retained as an optional workflow for demonstrating the annotation process.

## Interpretation

High classification accuracy on the BBC held-out test set does not guarantee similar performance on current external news.

Model confidence values are probability estimates and may not be calibrated.

Entity co-occurrence indicates shared article context, not verified relationships between entities.
