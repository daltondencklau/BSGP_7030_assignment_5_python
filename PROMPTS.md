# PROMPTS.md — Assignment 5a (Python, AI-Generated)

This file documents the prompting used to generate `notebook.ipynb` in this repository, as
required for the Part B comparison in BSGP 7030 Assignment 5.

## High-level prompt given

> I am in a bioinformatics class and we are learning how to generate machine learning (ML)
> models. I completed part A without the use of AI, and part B is entirely AI. Here is the
> objective: "On an `ai/` branch in each repo, rebuild from scratch. Same dataset, same task, but
> you're doing a vibe-coding pass:
>
> 1. Open Cursor (or your tool) on a clean `ai/` folder.
> 2. Describe the goal in one paragraph: 'Given this dataset, build a notebook that loads it,
>    splits train/test, trains a few classifiers, evaluates them, and picks the best.
>    Reproducible env + README.'
> 3. Let the AI structure the project. Only intervene to fix things that break.
> 4. Commit `ai/notebook.ipynb`, `ai/environment.yml`, `ai/README_AI.md`, `ai/PROMPTS.md`.
>
> You're graded on: it runs end-to-end, performance is reasonable, the env reproduces." Please do
> not push or delete anything without my permission and let me know what questions you have.

That's the prompt, word for word, as given in conversation. It doesn't specify the dataset,
algorithms, notebook structure, or environment contents beyond what's in the objective above —
those were left up to the AI to decide, consistent with the "vibe-coding pass" framing. R was
covered by this same message (see `ai/partB/PROMPTS.md` for the R-side framing of what was
decided independently there).

## What the AI decided independently

- **Dataset:** iris flower dataset, matching the manual submission's tutorial (not explicitly
  requested in the prompt, but a reasonable default given prior conversation context and its
  status as the standard "hello world" dataset for this kind of tutorial).
- **Workflow structure:** environment check → load data → summarize → visualize (boxplots,
  histograms, scatter matrix) → 10-fold cross-validated comparison of six classifiers →
  final model fit and hold-out evaluation. This mirrors the general shape of Brownlee's
  well-known Python ML tutorial, without copying its code.
- **Algorithm choices:** Logistic Regression, LDA, KNN, CART, Naive Bayes, SVM — a standard
  spread of simple linear and nonlinear classifiers appropriate for a small multiclass dataset.
- **API choices that avoided errors hit in the manual notebook:** `LogisticRegression` was
  built with `solver='lbfgs'` rather than `liblinear` (which fails on multiclass problems in
  current scikit-learn), and `plt.boxplot()` used `tick_labels` rather than the deprecated
  `labels` argument. These were not explicitly prompted — the AI used current library knowledge
  rather than reproducing the exact tutorial code that caused version-drift errors in Part A.

## Observations for the comparison writeup

The AI-generated notebook ran cleanly on the first execution with no errors, in contrast to the
manual notebook, which required multiple rounds of debugging for library API changes
(`liblinear` multiclass support, `matplotlib` boxplot argument renaming). This isn't because the
AI "knows more" in a deep sense — it reflects that the AI was working from current library
documentation/knowledge rather than literally transcribing an older tutorial's exact code, which
is precisely where the tutorial's age caused friction in the manual process.
