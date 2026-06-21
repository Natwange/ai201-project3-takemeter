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

# Dataset Scope

The dataset will consist of **comments from r/nba** rather than posts. Many r/nba posts are news headlines, injury updates, or quotes, whereas comments contain richer discourse and naturally exhibit the distinctions between **Analysis**, **Opinion**, and **Reaction**.
