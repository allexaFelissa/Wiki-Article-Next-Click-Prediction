# Wikispeedia Next-Click Prediction

This repository contains the inference notebook for Task 2 of the Datathon competition:

<https://www.kaggle.com/competitions/datathon-task-2>

The notebook predicts the next article a user is likely to click while navigating the Wikispeedia article graph. It uses the current article, target article, article metadata, observed transitions, and a reconstructed article-link graph.

## Important: data is not stored in this repository

The notebook does not bundle the competition data. This keeps the repository small and avoids redistributing competition data. When run on Kaggle, attach the competition data to the notebook/kernel. The notebook expects these files to be available somewhere below `/kaggle/input/`:

- `states_train.csv`
- `states_test.csv`
- `articles.csv`
- `categories.csv`
- `graph_edges.parquet`

The first four files come from the [Datathon Task 2 competition](https://www.kaggle.com/competitions/datathon-task-2). `graph_edges.parquet` is the reconstructed Wikispeedia graph used by the model and must be attached as an additional Kaggle Dataset input.

## Run on Kaggle

1. Open the competition link above and accept the competition rules if required.
2. Create a Kaggle Notebook.
3. Add the competition data as an input.
4. Add the dataset containing `graph_edges.parquet` as another input.
5. Upload or copy `apa nyak_Task2_Notebook.ipynb` into the notebook.
6. Run all cells.

The notebook writes the predictions to `/kaggle/working/submission.csv`.

## Run locally or in Colab

Download the same five files from Kaggle and either run the notebook in Kaggle (the recommended path), or change the input directory in the first code cell from `/kaggle/input/` to the local directory containing the files.

Install the Python dependencies first:

```bash
pip install -r requirements.txt
```

The notebook has saved output cells so the approach and an example result can be reviewed directly on GitHub, but GitHub itself does not execute notebooks.

## Model summary

Candidates are the current page's real outgoing links. The model keeps candidates at minimum graph distance from the target and breaks ties using PageRank, TF-IDF similarity, forward progress toward the target, category-conditioned popularity, in-degree, and category match.
