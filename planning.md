# TakeMeter Planning

## Community Description

I chose **r/nba** because it is a highly active community where fans discuss players, teams, trades, and league events. The labels **Analysis**, **Opinion**, and **Reaction** capture different styles of discourse that NBA fans commonly recognize, ranging from reasoned arguments to personal judgments and emotional responses. These distinctions matter because conversations in sports communities often vary not only in what people believe, but in how they communicate those beliefs.

---

# Label Taxonomy

## 1. Analysis

### Definition

A comment that supports a claim using reasons, evidence, comparisons, or cause-and-effect explanations.

### Clear Examples

#### Example 1

> While Dort wasn't amazing this last season, he's still an elite one-on-one defender and being able to just shoot open threes off Luka seems like his ideal offensive role. This would be a really good addition for the Lakers.

#### Example 2

> There is no early extension. He will opt out in two seasons to sign the same 35% cap supermax with any team. The Lakers can only offer a fifth year and larger annual raises, which is why Luka is essentially on an expiring contract.

### Uncertain Example

> Not enough people talk about how transformational the Starburys were. Dope ass comfy shoes that were $20 and no one had to feel embarrassed to rock them. A superstar signature shoe that everyone can afford should be the standard.

#### Possible Labels

- Analysis
- Opinion

#### Decision Rule

If the comment provides multiple reasons that explain why the conclusion is true, label it **Analysis**. If it mainly expresses approval or disapproval with little supporting reasoning, label it **Opinion**.

---

## 2. Opinion

### Definition

A comment expressing a judgment, preference, or prediction with little supporting reasoning.

### Clear Examples

#### Example 1

> Obama is probably the only other politician I would trust to give this good of a basketball related speech.

#### Example 2

> Cade is a stud and with a little more scoring support the Pistons will be back in the playoffs next season.

### Uncertain Example

> After losing to the Knicks, instead of congratulating their opponents they headed straight to the locker room. Total lack of class and maturity from the Spurs.

#### Possible Labels

- Opinion
- Analysis

#### Decision Rule

If the evidence consists of a single observation that mainly serves to justify a judgment, label it **Opinion**. If the comment develops the claim with several reasons or comparisons, label it **Analysis**.

---

## 3. Reaction

### Definition

A comment that primarily expresses emotions, hype, praise, jokes, frustration, or disbelief without attempting to justify a claim.

### Clear Examples

#### Example 1

> I will never allow your slander in my presence goat.

#### Example 2

> Say it with me, everyone! Everybody is better than Jalen Brunson until it's time to be better than Jalen Brunson! 💪🏾

### Uncertain Example

> King of New York.

#### Possible Labels

- Reaction
- Opinion

#### Decision Rule

If the comment is primarily hype, celebration, or emotional expression, label it **Reaction**. If it is making a serious judgment or comparison, label it **Opinion**.

---

# Mutual Exclusivity

Most r/nba comments can be assigned to exactly one label. The primary source of ambiguity occurs between **Analysis** and **Opinion**, since both contain judgments. To address this, comments with multiple supporting reasons, comparisons, or explanations are labeled **Analysis**, while comments that simply state a belief or prediction with minimal support are labeled **Opinion**. **Reaction** comments are generally distinct because they emphasize emotion rather than argument.

---

# Anticipated Edge Cases

### Analysis vs. Opinion

Comments that contain a judgment and a small amount of supporting evidence can be difficult to classify.

#### Example

> After losing to the Knicks, instead of congratulating their opponents they headed straight to the locker room. Total lack of class and maturity from the Spurs.

#### Decision Rule

A single observation used mainly to justify a judgment is labeled **Opinion**. Comments containing multiple reasons, evidence, or comparisons are labeled **Analysis**.

---

### Reaction vs. Opinion

Short celebratory comments and praise may resemble opinions.

#### Example

> King of New York.

#### Decision Rule

Comments whose primary purpose is hype, celebration, or emotional expression are labeled **Reaction**. Comments making a serious judgment or comparison are labeled **Opinion**.

---

# Data Collection Plan

## Source

Examples will be collected from **comments on r/nba**. Comments are preferred over posts because many posts are simply news headlines, injury updates, or quotes, whereas comments contain richer discourse and naturally exhibit the distinctions between **Analysis**, **Opinion**, and **Reaction**.

## Target Label Distribution

The dataset will contain at least **200 labeled examples** with the following target distribution:

| Label | Target Count |
|---------|------:|
| Analysis | 70 |
| Opinion | 70 |
| Reaction | 60 |

The exact distribution does not need to be perfectly balanced, but each label should represent at least 20% of the dataset to avoid severe class imbalance.

## Handling Underrepresented Labels

If one label is underrepresented after collecting 200 examples, additional comments will be collected until the label distribution becomes more balanced. Data collection will continue until each label contains enough examples for the model to learn meaningful distinctions.

---

# Evaluation Metrics

## Overall Accuracy

Accuracy measures the percentage of comments classified correctly. It provides a high-level view of performance but does not reveal how well the model performs on individual labels.

## Precision

Precision measures how often the model's predictions for a label are correct.

This is important because a community tool should avoid incorrectly labeling comments. For example, a reaction comment should not frequently be classified as analysis.

## Recall

Recall measures how many examples of a label the model successfully identifies.

This is important because the classifier should not consistently miss one type of discourse.

## F1 Score

F1 score balances precision and recall.

Since the three labels may not appear equally often, F1 score provides a more reliable measure than accuracy alone.

## Confusion Matrix

A confusion matrix will be used to identify which labels are commonly confused with one another.

This is especially important because the largest anticipated source of error is distinguishing **Analysis** from **Opinion**.

---

# Definition of Success

The classifier would be considered genuinely useful if:

- Overall accuracy is at least **80%**.
- Each label achieves an F1 score of at least **0.75**.
- No label has a recall below **70%**.
- Most errors occur between **Analysis** and **Opinion**, which are naturally difficult to separate.

For a real community tool, performance in this range would be good enough to provide useful information about discussion quality without requiring perfect predictions.

---

# Evaluation Criteria

Success criteria are specific and measurable.

At the end of the project, success can be objectively determined by examining:

1. Overall accuracy.
2. Precision, recall, and F1 scores for each label.
3. The confusion matrix.
4. Error analysis on incorrectly classified comments.

These metrics provide clear standards for determining whether the classifier achieved its intended goals.

---

# AI Tool Plan

## Label Stress-Testing

Before annotating the full dataset, AI tools will be used to generate comments that sit at the boundary between two labels.

Examples include:

- Analysis vs. Opinion
- Opinion vs. Reaction

If generated examples cannot be classified consistently, the label definitions and decision rules will be refined before annotation begins.

## Annotation Assistance

ChatGPT may be used to suggest labels for batches of comments.

However, all labels will be reviewed and assigned manually by myself. AI-generated suggestions will not be accepted without my verification.

Examples that were initially pre-labeled using AI assistance will be tracked separately and disclosed in the AI usage section of the final report.

## Failure Analysis

After evaluation, incorrectly classified comments will be given to ChatGPT to identify possible patterns.

Potential patterns include:

- Confusion between Analysis and Opinion.
- Short comments being mistaken for reactions.
- Predictions affected by sarcasm or humor.

Any patterns suggested by AI will be verified manually using the misclassified examples before being included in the final evaluation report.
