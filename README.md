
# NewsBot Intelligence System
### Domain-Specific NLP for News Classification and Intelligence

**Course:** ITAI 2373  
**Project:** Midterm Project (Individual Implementation) 
**Status:** Functional Academic Prototype  
**Technology:** Python, NLTK, spaCy, scikit-learn, VADER, NRCLex

## Project Overview

NewsBot Intelligence System is a domain-specific Natural Language Processing (NLP) prototype designed to transform unstructured news articles into structured, actionable information.

Rather than focusing only on category prediction, NewsBot combines eight NLP modules to analyze article topics, linguistic patterns, sentiment, emotion associations, named entities, and syntactic relationships.

The objective is to demonstrate how traditional NLP techniques and machine learning can work together to support automated content organization, media monitoring, and information discovery.

## Business Problem

News organizations and media analysts process large volumes of unstructured articles. Manually organizing content and identifying relevant information can be time-consuming and inconsistent.

NewsBot addresses this challenge by providing:

- Automated news classification
- Sentiment and emotion-association analysis
- Named entity extraction
- Linguistic and syntactic analysis
- Entity co-occurrence discovery
- Structured article insights

The system is intended as an academic prototype, not a production-ready news platform.

## Dataset

**Dataset:** BBC News Classification Dataset  
**Source:** [BBC News Dataset on Kaggle](https://www.kaggle.com/c/learn-ai-bbc/data)

| Description | Value |
|---|---:|
| Original records | 1,490 |
| Missing-value removals | 0 |
| Exact duplicates removed | 50 |
| Final articles | 1,440 |
| News categories | 5 |
| Training articles | 1,152 |
| Testing articles | 288 |

Categories:

1. Business
2. Entertainment
3. Politics
4. Sport
5. Tech

The dataset does not include original publication dates or independent article headlines. This limits temporal analysis and headline-specific evaluation.

## System Architecture

```text
News Article
    |
    v
Text Preprocessing
    |
    +------------------------+
    |                        |
    v                        v
TF-IDF Features       Linguistic Features
    |                  POS / Text Length
    +-----------+------------+
                |
                v
      Classification Pipeline
                |
                v
      Predicted News Category

Parallel Analysis:
    |
    +--> VADER Sentiment Analysis
    |
    +--> NRC Emotion Associations
    |
    +--> spaCy Named Entity Recognition
    |
    +--> Dependency and Syntax Analysis
                |
                v
      Structured NewsBot Insights
```

The classification pipeline uses TF-IDF alone for Naive Bayes. Logistic Regression and SVM configurations also incorporate numerical features.

## Eight NLP Modules

| Module | Implementation |
|---|---|
| 1. Business Context | Dataset exploration and problem definition |
| 2. Text Preprocessing | Cleaning, tokenization, stopword removal, lemmatization |
| 3. TF-IDF | Unigrams, bigrams, vocabulary and category terms |
| 4. POS Analysis | Grammatical patterns and writing-style comparison |
| 5. Syntax Analysis | Dependency parsing, noun phrases and action patterns |
| 6. Sentiment and Emotion | VADER polarity and NRC emotion associations |
| 7. Classification | Naive Bayes, Logistic Regression and SVM |
| 8. Named Entity Recognition | Entity extraction, frequency and co-occurrence |

## Classification Results

Three machine learning classifiers were evaluated using a stratified 80/20 train/test split and five-fold cross-validation.

Preprocessing transformations are fitted independently inside each cross-validation fold to prevent TF-IDF vocabulary and scaling leakage.

**Selected model: Multinomial Naive Bayes**

| Metric | Result |
|---|---:|
| Held-out test accuracy | 94.44% |
| Held-out macro F1 | 94.03% |
| Five-fold CV macro F1 | 97.01% |

Naive Bayes was selected using training cross-validation macro F1, rather than held-out test accuracy.

SVM achieved higher held-out accuracy in the model comparison, but the held-out test set was not used as the primary model-selection criterion.

The model configurations do not use identical feature sets. Their results should therefore be interpreted as comparisons of complete configurations rather than isolated classifier algorithms.

## Sentiment and Emotion Analysis

VADER estimates positive, neutral and negative sentiment, including a compound polarity score.

The NRC emotion experiment analyzes eight emotion associations:

- Anger
- Anticipation
- Disgust
- Fear
- Joy
- Sadness
- Surprise
- Trust

The experiment sampled 150 articles, with 30 from each news category.

All 150 sampled articles contained at least one matched emotion association in the saved experiment.

NRC scores describe lexical associations. They are not verified psychological emotions or measures of media bias.

## Named Entity Recognition

NewsBot uses spaCy to identify people, organizations, locations, dates, monetary values and other named entities.

Saved notebook results:

| Metric | Result |
|---|---:|
| Entity mentions | 40,803 |
| Entity types | 18 |
| Co-occurrence network nodes | 30 |
| Co-occurrence network edges | 222 |

Entity co-occurrence means two entities appeared within the same article. It does not establish a verified real-world relationship.

Manual NER review is performed on a 30-prediction sample. Review results are maintained separately from the automated extraction statistics.

## End-to-End NewsBot

The integrated prototype accepts a news article and returns:

- Predicted category
- Model-estimated category probabilities
- VADER sentiment scores
- Named entities
- Syntactic information
- Interpretable insights

The saved demonstration includes seven synthetic articles and two external-source examples.

All nine examples executed successfully. Both external predictions matched their manually assigned labels, but two examples are insufficient to establish external classification accuracy.

## Repository Structure

```text
.
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── Midterm_NewsBot_Intelligence_System.ipynb
├── data/
│   └── README.md
├── evaluation/
│   ├── README.md
│   ├── newsbot_ner_manual_review.csv
│   ├── newsbot_testing_results.csv
│   └── model_comparison.csv
├── results/
│   └── figures/
├── reports/
│   ├── Midterm_Report.pdf
│   └── NewsBot_Group_Reflection.pdf
└── demo/
    └── demo_video_link.md
```

Files not yet generated should be added only after they are available.

## How to Run

### Option A: Google Colab

1. Open `notebooks/NewsBot_Intelligence_System.ipynb`.
2. Select **Open in Colab** or upload the notebook to Google Colab.
3. Run the environment setup section.
4. Download the BBC News dataset from Kaggle if it is not already available.
5. Follow the dataset-loading instructions.
6. Run the notebook sections in order.
7. Inspect classification, sentiment, emotion and NER results.
8. Run the integrated NewsBot demonstration.

The interactive manual NER review is an optional annotation workflow. Instructors should be able to inspect the completed evaluation without repeating the manual review.

### Option B: Local Python

Create a virtual environment and install dependencies:

```bash
python -m venv .venv
pip install -r requirements.txt
python -m spacy download en_core_web_sm
```

Then open the notebook in Jupyter or VS Code.

Google Colab is the primary tested environment. Local compatibility may require adjustments to Colab-specific file paths and APIs.

## Limitations

- The BBC dataset may not represent current news writing styles.
- The dataset lacks publication dates and original headlines.
- Classification probabilities may not be calibrated.
- Short or ambiguous articles can be difficult to classify.
- VADER and NRC are lexicon-based approaches.
- spaCy named entity predictions may contain boundary and label errors.
- Entity co-occurrence does not prove real-world relationships.
- External evaluation uses a small number of examples.

## Future Improvements

1. Expand external evaluation with independently labeled news articles.
2. Calibrate classifier probabilities.
3. Compare additional feature combinations.
4. Improve domain-specific named entity recognition.
5. Incorporate real publication dates.
6. Add interactive search and article filtering.
7. Build a Streamlit or Gradio interface.

## Author
- Huong Thi Hue Nguyen

## Project Deliverables

- [Final Notebook](notebooks/NewsBot_Intelligence_System.ipynb)
- [Dataset Documentation](data/README.md)
- [Evaluation Documentation](evaluation/README.md)
- [Technical Report](reports/Midterm_Report.pdf)
- [Group Reflection](reports/NewsBot_Group_Reflection.pdf)
- [Demo Video](demo/demo_video_link.md)

## Academic Integrity and Reproducibility

All reported metrics are based on saved notebook experiments. The prototype's performance on new articles may differ from its held-out BBC test results.

Manual annotations, external test labels and model limitations are documented separately to avoid overstating evaluation quality.
