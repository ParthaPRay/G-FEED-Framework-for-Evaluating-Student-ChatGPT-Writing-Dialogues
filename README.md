# G-FEED Framework for Evaluating Student–ChatGPT Writing Dialogues

## Overview

This repository contains the implementation of the **G-FEED Framework**:  
**Generative Feedback Effectiveness and Educational Engagement Dialogue Framework**.

The framework is designed to evaluate the usefulness of GenAI feedback in student–ChatGPT writing dialogues. It focuses on how ChatGPT feedback can be analyzed through readability, linguistic complexity, pedagogical quality, student satisfaction, feedback uptake, and student-level interaction profiles.

The main notebook in this repository is:

```text
g-feedframework.ipynb
````

The notebook implements a complete Python-based workflow for analyzing student–ChatGPT interactions from the RECIPE4U dataset in the context of EFL writing education.

---

## Repository

GitHub Repository:

```text
https://github.com/ParthaPRay/G-FEED-Framework-for-Evaluating-Student-ChatGPT-Writing-Dialogues
```

---

## Framework Name

**G-FEED** stands for:

```text
Generative Feedback Effectiveness and Educational Engagement Dialogue Framework
```

The framework examines when GenAI-generated feedback becomes educationally useful by combining:

* readability analysis,
* linguistic complexity analysis,
* GPT-assisted pedagogical coding,
* feedback accessibility scoring,
* student satisfaction modelling,
* essay-edit uptake analysis,
* student-level interaction profiling,
* clustering and PCA-based visualization.

---

## Research Motivation

Generative AI tools such as ChatGPT are increasingly used in higher education writing tasks. However, simply knowing that students use GenAI is not enough. A more important question is:

> When does GenAI feedback actually become educationally useful?

The G-FEED framework addresses this question by studying the interaction between students and ChatGPT at the dialogue level. It does not treat ChatGPT feedback as a black box. Instead, it analyzes whether the feedback is readable, specific, empathetic, actionable, scaffolded, and supportive of self-regulated learning.

At the same time, the framework also examines potential risks, such as direct-answer dependency and encouragement of cognitive outsourcing.

---

## Dataset

This repository uses the **RECIPE4U dataset**, a student–ChatGPT interaction dataset developed for EFL writing education.

The dataset contains student–ChatGPT dialogue records, including student utterances, ChatGPT responses, satisfaction ratings, student-intent annotations, essay-edit indicators, quiz-related indicators, and essay text.

### Dataset Citation

Please cite the dataset as:

```text
Han, J., Yoo, H., Myung, J., Kim, M., Lee, T. Y., Ahn, S.-Y., & Oh, A. (2024). 
RECIPE4U: Student-ChatGPT interaction dataset in EFL writing education. 
In Proceedings of the 2024 Joint International Conference on Computational Linguistics, 
Language Resources and Evaluation (LREC-COLING 2024) (pp. 13666–13676). 
ELRA and ICCL. https://aclanthology.org/2024.lrec-main.1193
```

BibTeX format:

```bibtex
@inproceedings{han2024recipe4u,
  title     = {RECIPE4U: Student-ChatGPT Interaction Dataset in EFL Writing Education},
  author    = {Han, Jieun and Yoo, Haneul and Myung, Junho and Kim, Minjin and Lee, Tae Yoon and Ahn, So-Yeon and Oh, Alice},
  booktitle = {Proceedings of the 2024 Joint International Conference on Computational Linguistics, Language Resources and Evaluation (LREC-COLING 2024)},
  pages     = {13666--13676},
  year      = {2024},
  publisher = {ELRA and ICCL},
  url       = {https://aclanthology.org/2024.lrec-main.1193}
}
```

---

## Dataset Attributes

The RECIPE4U dataset includes the following key columns:

| Column                              | Description                                                                                          |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `sample_id`                         | Unique identifier composed of student ID, course, week, session, and utterance index                 |
| `course`                            | Course information such as Intermediate Reading and Writing, Advanced Writing, or Scientific Writing |
| `student_id`                        | Anonymized numerical student identifier                                                              |
| `week`                              | Week number of the conversation                                                                      |
| `session`                           | Session number within the week                                                                       |
| `idx`                               | Utterance index within the session                                                                   |
| `chatgpt_before`                    | ChatGPT utterance before the student's utterance                                                     |
| `user`                              | Student utterance after receiving ChatGPT feedback                                                   |
| `chatgpt_after`                     | ChatGPT response after the student's utterance                                                       |
| `rating`                            | Student self-rated satisfaction on a 5-point Likert scale                                            |
| `intent_final`                      | Annotation of the student's intention                                                                |
| `is_quiz`                           | Whether the student asked ChatGPT for a quiz answer                                                  |
| `is_essay_edit` / `is_essay_edited` | Whether the student edited the essay after receiving ChatGPT feedback                                |
| `essay`                             | Student's written essay                                                                              |

---

## Main Notebook

The main notebook is:

```text
g-feedframework.ipynb
```

This notebook performs the full G-FEED analysis pipeline.

---

## Main Components of the Framework

### 1. Data Cleaning and Preprocessing

The notebook first loads the RECIPE4U dataset and prepares it for analysis. Text columns are cleaned and standardized. Numeric variables are converted into usable formats. Binary variables such as essay-edit uptake are constructed for modelling.

The workflow creates interaction-level variables such as:

* student prompt word count,
* ChatGPT response word count,
* essay length,
* satisfaction rating,
* essay-edit uptake indicator.

---

### 2. Readability and Linguistic Complexity Analysis

The framework computes readability and complexity metrics for ChatGPT responses and student prompts.

The implemented readability and linguistic metrics include:

* Flesch Reading Ease,
* Flesch–Kincaid Grade Level,
* SMOG Index,
* Coleman–Liau Index,
* Automated Readability Index,
* Dale–Chall Readability Score,
* Gunning Fog Index,
* difficult-word count,
* syllable count,
* sentence count,
* character count,
* lexicon count,
* estimated reading time.

These metrics help examine whether ChatGPT feedback is accessible and understandable to students.

---

### 3. Feedback Accessibility Index

The notebook constructs a feedback accessibility index by combining standardized readability and linguistic complexity information.

The basic idea is:

```text
Higher accessibility = higher readability and lower linguistic complexity
```

This index is used to evaluate whether more accessible ChatGPT feedback is associated with student satisfaction or essay-edit uptake.

---

### 4. GPT-Assisted Pedagogical Coding

A key contribution of the G-FEED framework is the GPT-assisted pedagogical coding layer.

Using the OpenAI API, each ChatGPT response can be coded on multiple pedagogical dimensions:

* clarity,
* specificity,
* empathy,
* self-regulation support,
* scaffolding,
* direct-answer tendency,
* dependency-risk encouragement,
* actionability,
* feedback depth,
* non-judgmental tone.

This step moves beyond surface readability and evaluates whether ChatGPT feedback is pedagogically useful.

---

### 5. Pedagogical Indices

The notebook constructs several composite indices from the GPT-coded dimensions:

| Index                            | Meaning                                                                                                                             |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Positive Feedback Quality Index  | Average of constructive pedagogical qualities such as clarity, specificity, empathy, scaffolding, actionability, and feedback depth |
| Dependency-Risk Index            | Average of direct-answer tendency and dependency-risk encouragement                                                                 |
| G-FEED Pedagogical Utility Index | Positive feedback quality minus dependency risk                                                                                     |
| SRL Scaffolding Index            | Average of self-regulation support, scaffolding, and actionability                                                                  |

These indices help evaluate whether ChatGPT feedback supports productive student engagement or risks promoting over-reliance.

---

### 6. Student Satisfaction Analysis

The framework examines how readability, feedback accessibility, and GPT-coded pedagogical quality relate to student satisfaction ratings.

The notebook includes:

* descriptive statistics,
* correlation analysis,
* ordinary least squares regression,
* robust standard errors,
* intent-controlled models.

This helps investigate what kinds of feedback properties are associated with higher student satisfaction.

---

### 7. Essay-Edit Uptake Analysis

The notebook also examines whether students edited their essays after receiving ChatGPT feedback.

Essay-edit uptake is treated as an observable proxy for feedback use.

The analysis includes:

* edited versus non-edited comparisons,
* Mann–Whitney U tests,
* false discovery rate correction,
* logistic regression,
* robust or regularized logistic modelling when necessary.

This part of the framework helps examine whether certain feedback features are associated with actual student revision behaviour.

---

### 8. Student-Level Interaction Profiling

Because students may have multiple interactions, the notebook aggregates data at the student level.

Student-level variables include:

* number of interactions,
* mean rating,
* essay-edit rate,
* mean student prompt length,
* mean ChatGPT response length,
* mean readability,
* mean linguistic complexity,
* mean feedback accessibility,
* number of distinct intent labels.

These features are used to identify student interaction profiles.

---

### 9. Clustering and PCA Visualization

The framework applies clustering and PCA to explore student-level interaction patterns.

The notebook includes:

* standardized student-level features,
* k-means clustering,
* silhouette-score-based cluster selection,
* PCA visualization of student interaction profiles.

This allows the framework to identify groups of students who may differ in how they interact with ChatGPT feedback.

---

## Methodological Workflow

The G-FEED workflow can be summarized as follows:

```text
RECIPE4U Student–ChatGPT Dialogues
        ↓
Data Cleaning and Interaction-Level Feature Construction
        ↓
Readability and Linguistic Complexity Analysis
        ↓
Feedback Accessibility Index
        ↓
GPT-Assisted Pedagogical Coding
        ↓
Pedagogical Quality and Dependency-Risk Indices
        ↓
Satisfaction and Essay-Edit Uptake Modelling
        ↓
Student-Level Aggregation
        ↓
Clustering and PCA-Based Interaction Profiling
        ↓
Evidence-Based Interpretation of GenAI Feedback Usefulness
```

---

## Software and Libraries

The notebook uses Python and the following major libraries:

```text
pandas
numpy
scipy
statsmodels
scikit-learn
matplotlib
seaborn
textstat
openpyxl
xlsxwriter
tqdm
openai
```

Optional libraries used for extended linguistic analysis:

```text
spacy
textdescriptives
```

---

## OpenAI API Use

The GPT-assisted pedagogical coding layer uses the OpenAI API.

The API is used to code ChatGPT feedback responses according to a fixed educational rubric. The OpenAI API is not used to replace the dataset. It is used only as a structured annotation tool for analysing pedagogical properties of existing ChatGPT responses.

The notebook is designed to request the API key securely during execution.

---

## Outputs Generated by the Notebook

The notebook generates several publication-oriented outputs, including:

* cleaned dataset files,
* readability metric tables,
* satisfaction distribution tables,
* essay-edit uptake tables,
* intent-wise summary tables,
* correlation matrices,
* regression tables,
* GPT-coded pedagogical score tables,
* edited versus non-edited comparison tables,
* student-level aggregation tables,
* clustering tables,
* PCA coordinate tables,
* publication-quality figures,
* statistical summary text files,
* combined Excel workbooks,
* downloadable ZIP archives.

---

## Research Contribution

The G-FEED framework contributes a structured method for evaluating GenAI feedback in educational dialogue data. It combines computational readability analysis, GPT-assisted pedagogical coding, statistical modelling, and student-level profiling.

The framework is useful for studying questions such as:

* When is ChatGPT feedback readable and accessible?
* When is ChatGPT feedback pedagogically useful?
* Which feedback properties are associated with student satisfaction?
* Which feedback properties are associated with essay-edit uptake?
* Does ChatGPT feedback scaffold student revision or encourage dependency?
* Can student interaction profiles reveal different patterns of GenAI engagement?

---

## Important Interpretation Notes

This repository does not claim that ChatGPT feedback directly causes learning gains. The dataset does not contain direct pre-test or post-test learning measures.

The framework uses observable indicators such as:

* satisfaction rating,
* essay-edit uptake,
* student intent,
* response readability,
* GPT-coded pedagogical quality,
* interaction frequency,
* student-level usage profile.

Therefore, the results should be interpreted as evidence about student–GenAI interaction patterns and feedback usefulness, not as direct proof of cognitive learning improvement.

---

## Suggested Citation for This Repository

If you use this framework or notebook, please cite this repository as:

```text
Ray, P. P. (2026). G-FEED Framework for Evaluating Student–ChatGPT Writing Dialogues. 
GitHub repository. https://github.com/ParthaPRay/G-FEED-Framework-for-Evaluating-Student-ChatGPT-Writing-Dialogues
```

BibTeX:

```bibtex
@misc{ray2026gfeed,
  author       = {Ray, Partha Pratim},
  title        = {G-FEED Framework for Evaluating Student--ChatGPT Writing Dialogues},
  year         = {2026},
  howpublished = {GitHub repository},
  url          = {https://github.com/ParthaPRay/G-FEED-Framework-for-Evaluating-Student-ChatGPT-Writing-Dialogues}
}
```

---

## License

Please add an appropriate license before public reuse.

Recommended options:

* MIT License for code,
* CC BY 4.0 for documentation,
* dataset reuse subject to the original RECIPE4U dataset terms and citation requirements.

---

## Author

**Partha Pratim Ray**
Department of Computer Applications
Sikkim University, India

GitHub: [ParthaPRay](https://github.com/ParthaPRay)

---

## Acknowledgement

This repository uses the RECIPE4U dataset. The dataset creators should be cited appropriately in any derivative research or publication.

Dataset citation:

```text
Han, J., Yoo, H., Myung, J., Kim, M., Lee, T. Y., Ahn, S.-Y., & Oh, A. (2024). 
RECIPE4U: Student-ChatGPT interaction dataset in EFL writing education. 
In Proceedings of the 2024 Joint International Conference on Computational Linguistics, 
Language Resources and Evaluation (LREC-COLING 2024) (pp. 13666–13676). 
ELRA and ICCL. https://aclanthology.org/2024.lrec-main.1193
```

```
```
