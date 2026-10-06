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
