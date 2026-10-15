
# Dataset Documentation

## Dataset Overview

NewsBot uses the BBC News Classification Dataset from the Kaggle Learn AI BBC competition.

**Source:** https://www.kaggle.com/c/learn-ai-bbc/data

The dataset contains English-language news articles classified into five categories:

- Business
- Entertainment
- Politics
- Sport
- Tech

## Dataset Statistics

| Metric | Value |
|---|---:|
| Original records | 1,490 |
| Missing-value removals | 0 |
| Exact duplicate removals | 50 |
| Final records | 1,440 |
| Categories | 5 |

The final dataset contains unique article content after exact duplicate removal.

## Data Preparation

The preprocessing workflow includes:

1. Load the original CSV.
2. Validate the content and category columns.
3. Remove missing article content or labels.
4. Remove exact duplicate article content.
5. Normalize category labels.
6. Generate article identifiers and title proxies.
7. Apply text cleaning, tokenization and lemmatization.
8. Prepare classification features.

## Train/Test Split

The dataset is split using stratified sampling:

- Training: 1,152 articles (80%)
- Testing: 288 articles (20%)
- Random state: 42

TF-IDF vectorization and numerical scaling are fitted inside the training pipeline.

Cross-validation uses five stratified folds.

## Download Instructions

1. Visit https://www.kaggle.com/c/learn-ai-bbc/data
2. Sign in to Kaggle.
3. Accept any applicable competition conditions.
4. Download the BBC News training CSV.
5. Save it as `BBC News Train.csv`.
6. Follow the notebook's dataset-loading instructions.

## Data Availability

The original dataset is maintained by its source provider.

Redistribution of the CSV should follow the applicable Kaggle competition and dataset terms.

If the CSV is not included in this repository, download it directly from Kaggle.

## Known Limitations

The dataset does not provide original publication dates or independent article headlines.

The notebook generates title proxies for feature analysis. These should not be interpreted as authentic published headlines.

Exact duplicate removal does not guarantee that near-duplicate reports or closely related articles are absent.

The BBC news collection may not represent modern reporting styles or all news publishers.

## Dataset Approval

Dataset: BBC News Classification Dataset

Source: https://www.kaggle.com/competitions/learn-ai-bbc/data

The BBC News Classification Dataset is one of the datasets recommended in the midterm assignment instructions.

The prepared dataset contains 1,440 English news articles across five categories.
