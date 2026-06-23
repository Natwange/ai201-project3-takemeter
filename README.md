# TakeMeter: Classifying NBA Discourse Quality

## Overview

TakeMeter is a text classification project that analyzes discourse in the r/nba community. The goal is to classify NBA discussion comments into one of three categories:

* **Analysis** – comments that support claims using evidence, comparisons, or reasoning.
* **Opinion** – comments that express judgments, preferences, or predictions with little supporting reasoning.
* **Reaction** – comments that primarily express emotions, hype, humor, frustration, or disbelief.

This project explores whether a fine-tuned language model can learn these distinctions more effectively than a zero-shot large language model.

---

## Community

This project uses comments collected from **r/nba**, one of Reddit's largest sports communities.

I selected r/nba because it contains a wide range of discourse styles. Fans regularly post detailed basketball analysis, personal opinions about players and teams, and emotional reactions to games and news. These distinctions are meaningful to community members and provide a useful classification task.

---

## Label Taxonomy

### Analysis

A comment that supports a claim using reasons, evidence, comparisons, statistics, or cause-and-effect explanations.

**Example**

> While Dort wasn't amazing this last season, he's still an elite one-on-one defender and being able to just shoot open threes off Luka seems like his ideal offensive role. This would be a really good addition for the Lakers.

---

### Opinion

A comment expressing a judgment, preference, or prediction with little supporting reasoning.

**Example**

> Obama is probably the only other politician I would trust to give this good of a basketball related speech.

---

### Reaction

A comment that primarily expresses emotions, hype, praise, jokes, frustration, excitement, or disbelief without attempting to justify a claim.

**Example**

> I will never allow your slander in my presence goat.

---

## Dataset

### Data Source

All examples were collected from public comments on **r/nba**.

### Dataset Size

| Label     |   Count |
| --------- | ------: |
| Analysis  |      70 |
| Opinion   |      61 |
| Reaction  |      69 |
| **Total** | **200** |

### Annotation Process

All 200 comments were manually labeled according to the taxonomy defined in `planning.md`.

Difficult examples were reviewed against the project's decision rules to ensure consistency. Particular attention was given to comments that sat between the Analysis and Opinion labels.

### Difficult Examples

#### Example 1

> Not enough people talk about how transformational the Starburys were. Dope ass comfy shoes that were $20 and no one had to feel embarrassed to rock them.

Possible labels:

* Analysis
* Opinion

Decision:

Labeled as **Analysis** because the comment provides multiple reasons supporting its claim.

---

#### Example 2

> King of New York.

Possible labels:

* Opinion
* Reaction

Decision:

Labeled as **Reaction** because the comment functions primarily as hype and celebration rather than a serious judgment.

---

#### Example 3

> After losing to the Knicks, instead of congratulating their opponents they headed straight to the locker room. Total lack of class and maturity from the Spurs.

Possible labels:

* Opinion
* Analysis

Decision:

Labeled as **Opinion** because it contains a judgment supported by a single observation rather than a developed argument.

---

## Model

### Base Model

* DistilBERT (`distilbert-base-uncased`)

### Training Approach

The model was fine-tuned on the labeled r/nba dataset using supervised learning.

### Hyperparameters

* Epochs: 7
* Model: DistilBERT Base Uncased
* Task: Multi-class text classification

The number of epochs was increased from 3 to 7 after initial training produced low accuracy.

---

# Evaluation Report

## Baseline vs Fine-Tuned Performance

### Baseline Model (Groq Zero-Shot)

| Label    | Precision | Recall | F1 Score |
| -------- | --------: | -----: | -------: |
| Analysis |      0.88 |   0.64 |     0.74 |
| Opinion  |      0.00 |   0.00 |     0.00 |
| Reaction |      0.53 |   1.00 |     0.69 |

**Overall Accuracy:** 56.7%

### Fine-Tuned DistilBERT Model

| Label    | Precision | Recall | F1 Score |
| -------- | --------: | -----: | -------: |
| Analysis |      0.58 |   1.00 |     0.73 |
| Opinion  |      0.00 |   0.00 |     0.00 |
| Reaction |      0.73 |   0.80 |     0.76 |

**Overall Accuracy:** 63.3%

**Improvement Over Baseline:** +6.6 percentage points

---

## Fine-Tuned Model Confusion Matrix

| True Label | Predicted Analysis | Predicted Opinion | Predicted Reaction |
| ---------- | ------------------ | ----------------- | ------------------ |
| Analysis   | 11                 | 0                 | 0                  |
| Opinion    | 6                  | 0                 | 3                  |
| Reaction   | 2                  | 0                 | 8                  |

---

## Sample Classifications

| Comment                                                          | Prediction | Confidence |
| ---------------------------------------------------------------- | ---------- | ---------: |
| "There is no early extension. He will opt out in two seasons..." | Analysis   |       0.58 |
| "King of New York"                                               | Reaction   |       0.48 |
| "Best coach ever"                                                | Reaction   |       0.41 |
| "Steph deserves 10x for what he did for the Warriors."           | Analysis   |       0.49 |

Example of a correct prediction:

> "There is no early extension. He will opt out in two seasons..."

The Analysis prediction is reasonable because the comment presents multiple supporting facts and uses them to reach a conclusion.

---

## Error Analysis

### Error 1

**Comment**

> Steph deserves 10x for what he did for the Warriors. Gonna be a terribly sad day when he hangs em up.

**True Label:** Opinion

**Predicted Label:** Analysis

This comment expresses a personal judgment about Steph Curry and his importance to the Warriors. While it contains a brief justification, it does not provide evidence, comparisons, statistics, or structured reasoning. The model appears to associate justification language with Analysis even when the comment is primarily expressing an opinion.

---

### Error 2

**Comment**

> Best coach ever

**True Label:** Opinion

**Predicted Label:** Reaction

This comment is a judgment rather than an emotional reaction. However, because it is extremely short and lacks supporting details, the model likely associated its brevity with Reaction comments.

---

### Error 3

**Comment**

> UTTER DISBELIEF: The least talented offensive player on an absurdly stacked team isn't regularly getting an arbitrary number of assists wwwoooaaahhh

**True Label:** Reaction

**Predicted Label:** Analysis

This comment is sarcastic and intended as mockery. Humans can recognize the exaggerated language and sarcasm as an emotional reaction, but the model appears to focus on the literal content rather than the intended tone.

---

## Error Patterns

The most common error pattern was **Opinion → Analysis**.

Six of the nine Opinion examples were classified as Analysis. The model appears to associate strong claims and explanatory language with Analysis, even when those comments are ultimately expressing personal judgments.

The second most common pattern was **Opinion → Reaction**. Short Opinion comments were often classified as Reaction because they were brief and emotionally charged.

---

## Reflection

The fine-tuned model improved overall accuracy from **56.7%** to **63.3%**, demonstrating that fine-tuning on community-specific examples helped the model learn some discourse patterns.

However, the model continued to struggle with Opinion comments and achieved an F1 score of 0.00 on that label. This suggests that the boundary between Opinion and Analysis remained difficult for the model to learn.

The model appears to have learned a simplified rule:

> Strong claim + explanation = Analysis

rather than the intended distinction between a personal judgment and a structured argument. As a result, many Opinion comments were absorbed into the Analysis category.

This project demonstrated that label design is often more important than model architecture. The greatest challenge was not training the classifier, but defining categories that were consistent enough for both humans and the model to apply reliably.

---

## Spec Reflection

The project specification helped guide my implementation by emphasizing the importance of label design before model training. Spending time defining decision rules and edge cases prevented many annotation inconsistencies that would have negatively affected model performance.

One way my implementation diverged from the original expectation was in the amount of effort devoted to refining the Opinion label. While the specification assumes labels can be defined clearly before annotation begins, I found that the boundary between Opinion and Analysis remained difficult even after collecting 200 examples. Much of the project became an exercise in understanding and refining label boundaries rather than simply training a classifier.

---

## AI Usage

### Label Validation During Annotation

After collecting comments from r/nba, I manually labeled all 200 examples according to my taxonomy. I then removed the labels and asked ChatGPT to independently classify the same comments.

I reviewed all disagreements manually. In some cases I agreed with ChatGPT and updated my labels. In other cases I determined that my original label better matched the project's decision rules and kept my original annotation.

### Label Stress Testing

Before completing annotation, I used ChatGPT to generate comments that sat near the boundary between Analysis, Opinion, and Reaction. These examples helped identify ambiguous cases and refine my decision rules.

### Failure Analysis

After evaluating the model, I provided misclassified examples to ChatGPT and asked it to identify possible error patterns. ChatGPT suggested that many errors involved Opinion comments being confused with Analysis and that sarcastic comments were difficult for the model.

I verified these patterns manually by reviewing the confusion matrix and individual examples before including them in the evaluation report.

---

## Demo Video

**Demo Link:** [DEMO VIDEO LINK](https://www.loom.com/share/0291b7a7c12b4035a8eeb7b3f82c847b)

The demo includes:

* Multiple comments classified by the fine-tuned model.
* Two correct prediction and explanation.
* Two incorrect prediction and analysis.
* A walkthrough of the evaluation report and findings.

