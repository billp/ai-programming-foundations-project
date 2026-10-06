# AI Programming Foundations Project

## Project Description

A reproducible data workflow in Python that loads, cleans, explores and visualizes the Titanic passenger dataset to see which passenger characteristics (sex, class, age, fare) are linked to survival. The workflow is built from small, documented functions so every step can be rerun from scratch, and it forms the base for the later machine learning and AI projects in the capstone.

## What I Built

- `data_workflow.ipynb`: the full workflow (data loading, cleaning functions, exploratory analysis functions, three visualizations and a written summary)
- `figures/`: the three charts produced by the notebook
- `requirements.txt`: the exact package versions used

## Dataset

**Titanic passengers** (891 rows, 15 columns), from the [seaborn-data repository](https://github.com/mwaskom/seaborn-data/blob/master/titanic.csv), a version of the [Kaggle Titanic dataset](https://www.kaggle.com/c/titanic/data).

The notebook loads the dataset automatically from a fixed link (pinned to a specific commit), so no download is needed. An internet connection is required the first time it runs.

## How to Run the Project

Requires Python 3.9 or higher.

1. Clone the repository:
   ```bash
   git clone https://github.com/billp/ai-programming-foundations-project.git
   cd ai-programming-foundations-project
   ```
2. Create and activate a virtual environment:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate        # Windows: .venv\Scripts\activate
   ```
3. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Open the notebook:
   ```bash
   jupyter notebook data_workflow.ipynb
   ```
5. Run all cells: **Run → Run All Cells**.

To regenerate `requirements.txt` after adding packages:
```bash
pip freeze > requirements.txt
```

## Reflection Questions

### 1. Bias awareness: where could poor data cleaning introduce bias?

In this dataset, the riskiest step is handling missing ages. Ages are missing for 19.9% of passengers, but far more often in third class (27.7%) than in first (13.9%) or second (6.0%). If I had simply dropped passengers without an age, I would have removed a large part of third class, the group with the lowest survival, and the overall survival rate would look higher than it really was. Filling every missing age with one overall value (28) would also mislead, because third-class passengers were younger and first-class passengers older, so the guess would be wrong in opposite directions for different groups. I reduced this risk by using the median age of passengers of the same class and sex, adding an `age_was_missing` flag, and drawing the age chart from recorded ages only. Deleting the 107 rows that look like duplicates would have been another mistake: without names or IDs they are most likely different people, and removing them would quietly change the group sizes.

### 2. How would this workflow change for a machine learning project?

The cleaning functions would stay, but they would be applied differently. The data would be split into training and test sets *before* any imputation, and values such as the median ages would be learned from the training set only, then applied to the test set, so no information leaks from the test data into the model. The steps would be wrapped in a reusable pipeline (for example scikit-learn's `Pipeline`) so exactly the same transformations run during training and prediction. Exploratory analysis would also guide feature choices, for example keeping `age_was_missing` as a feature and dropping columns that repeat others, as this workflow already does.

### 3. How would you prepare this data for a neural network?

Neural networks need all inputs to be numbers on similar scales. Categorical columns such as `sex` and `embarked` would be one-hot encoded, `pclass` could be encoded as categories rather than treated as a plain number, and numeric columns such as `age` and `fare` would be scaled (for example standardized), with `fare` log-transformed first because it is very skewed (as Figure 3 shows). Missing values must be filled in before training because a network cannot handle them, and the target `survived` stays as 0/1 for binary classification. With only 891 rows, a small network and careful validation would be needed to avoid overfitting.

### 4. Which parts of this workflow could be automated by an AI agent?

Repetitive and rule-based steps are good candidates: loading the data, running `report_missing` and the duplicate checks, applying the cleaning pipeline, regenerating the summary tables and figures, and checking that the notebook still runs from top to bottom after every change. An agent could also draft a first data-quality report, flagging high-missing columns, skewed variables and redundant columns. Decisions that need judgement should stay with a person, such as choosing how to impute, deciding that look-alike rows are real passengers, and interpreting results for bias, because these choices change what the data says and need to be justified.
