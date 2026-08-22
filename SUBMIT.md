# Project 1 — how to submit

Everything is built and the notebook has been run clean: 11 code cells, zero errors,
three figures rendered. Read the README and module_summary before you push — make the
words yours where you disagree with them.

## Files in this folder

| File | What it is |
|---|---|
| `data_workflow.ipynb` | The notebook, already executed with outputs saved |
| `module_summary.pdf`  | The academic report — 2 cited sources, all 8 required sections |
| `module_summary.md`   | Editable source for the PDF, in case you change anything |
| `README.md`           | Short run instructions plus all four rubric reflection answers |
| `requirements.txt`    | Package environment |
| `titanic.csv`         | The dataset |

## Step 1 — create the GitHub repo

Go to github.com, create a new repository named **exactly**:

    ai-programming-foundations-project

Public. Do not add a README, licence or .gitignore — this folder already has what it needs.

## Step 2 — run this block

Open a terminal in this folder and paste the whole thing at once. It creates the
multiple commits and the second branch that the rubric requires.

    git init
    git add titanic.csv requirements.txt
    git commit -m "Add dataset and environment"
    git add data_workflow.ipynb
    git commit -m "Add data workflow notebook: ingestion, cleaning, EDA, visualisations"
    git add README.md
    git commit -m "Add README with run instructions and reflections"
    git add module_summary.md module_summary.pdf
    git commit -m "Add module summary report with citations"
    git branch -M main
    git checkout -b development
    git checkout main
    git remote add origin https://github.com/YOUR-USERNAME/ai-programming-foundations-project.git
    git push -u origin main
    git push origin development

Replace `YOUR-USERNAME` with your GitHub username. Nothing else changes.

That gives you four commits on `main` and a `development` branch — both rubric
requirements met.

## Step 3 — submit on Udacity

learn.udacity.com/cd001-capstone → AI Programming Foundations Project → Submit Project.

Give the repository link.

## Before you press submit

Pass first time and you score 100%. Every resubmission after that takes 10% off, and
every attempt appears on your transcript. The full 16-criterion rubric is on SharePoint at
`00_PORTFOLIO_CONTROL/SOURCE_MATERIAL/UDACITY/TIER3_CAPSTONE/P1_AI_Programming_Foundations_RUBRIC.md`
