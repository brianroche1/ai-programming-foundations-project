# AI Programming Foundations Project

**Repository:** https://github.com/brianroche1/ai-programming-foundations-project
**Branches:** `main` (default) and `development`
**Version control:** the work was built across multiple commits — dataset and environment, notebook, README, then the module summary report — with the `development` branch used for subsequent revision and merged into `main` through pull request #1.

## Project Description

A reusable Python data workflow built on the Titanic passenger manifest: ingestion with
pandas, cleaning through two documented functions, exploration through a single reusable
analysis function, and three labelled visualisations. The dataset was chosen because its
missing data is structurally varied — one column missing 20% of values, another missing 77%,
a third missing two rows — which makes cleaning a genuine engineering decision rather than a
formality.

## Dataset

Titanic passenger manifest — 891 rows, 12 columns.
https://raw.githubusercontent.com/datasciencedojo/datasets/master/titanic.csv

## How to Run

Clone the repository:

    git clone https://github.com/brianroche1/ai-programming-foundations-project.git
    cd ai-programming-foundations-project

Install dependencies:

    pip install -r requirements.txt

Open and run the notebook:

    jupyter notebook data_workflow.ipynb

Run all cells from top to bottom. `titanic.csv` must be in the same folder.

## Reflection — Bias Awareness

Poor cleaning would have introduced bias in this dataset in three specific ways.

**Imputing age with a single global median.** Age distribution differs sharply by class and
sex — a global median would have flattened that real variation and pulled every imputed
passenger toward one number. The workflow imputes within `Pclass` and `Sex` groups instead.
Even so, 177 imputed values concentrate mass in the age histogram, and Figure 2 shows it.

**Deleting rows with missing values.** Dropping incomplete rows would have removed 708 of 891
passengers, and not at random: third-class passengers are far likelier to be missing a cabin
record. The surviving sample would have been disproportionately wealthy, and every survival
rate computed from it would have been wrong in a predictable direction.

**Discarding the `Cabin` column outright.** At 77% missing the instinct is to delete it. But
the missingness is not noise — passengers with a recorded cabin survived at 66.7% against
30.0% for those without. Deleting the column would have destroyed a real signal; imputing
cabin numbers would have fabricated data. Preserving the *fact* of the record as a binary
flag keeps the signal without inventing anything.

## Reflection — Future Integration

### How would this workflow change for a machine learning project?

The cleaning and feature-derivation functions stay, but they move behind a fitted pipeline so
that imputation parameters are learned on the training split alone. As written,
`clean_missing_values` computes group medians over the whole dataset, which leaks information
from test into train. A modelling version would fit the imputer on the training fold and
apply it to the others. Categorical variables would need encoding, `SibSp` and `Parch` would
be dropped in favour of the derived `FamilySize`, and the EDA function would be joined by a
held-out evaluation step.

### How does this prepare the data for a neural network?

Three things are already in place: no missing values, correct types, and derived features
that carry combined signal. Three are not. Numeric ranges are wildly different — `Fare` spans
0 to 512 while `IsAlone` is 0 or 1 — so scaling is required before training. Categorical
variables need one-hot or embedding representation rather than pandas category dtype. And at
891 rows the dataset is far too small for a deep network to beat a simple model, so the
honest preparation step is to recognise that a neural network is the wrong tool here.

### Where could this workflow be automated by an agentic system?

The mechanical stages automate cleanly: profiling a new file, reporting missingness by
column, proposing type corrections, and generating the standard summary and plots. What does
not automate is the decision in the middle. Choosing to preserve `Cabin` as a flag rather
than impute or delete it was a judgement about *why* the data was missing, and it produced
the most interesting result in the project. An agent could surface the three options and the
consequences of each; a person still has to choose.

---
Full explanation and academic citations are in `module_summary.pdf`.
