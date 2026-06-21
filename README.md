# r/swimming Post Classification

## Community

The community chosen was the swimming subreddit ([r/swimming](https://www.reddit.com/r/swimming/)). This community was selected because it contains posts from a wide variety of users, ranging from ex-Olympians to recreational swimmers.

This community is a good fit for a classification task since posts span multiple purposes: giving advice, asking for advice, stating facts, sharing news, and more.

---

## Labels

### Advice
The post gives a suggestion to the channel. It can be based on personal experience or fact — evidence is not necessary. The advice can be general or targeted to a specific group.

**Examples:**
- *"You're not fading in the back half because you're unfit. You're going out too fast. Quick intro so you know why I'm writing this: I swam distance freestyle internationally. 800/1500 free, raced for Portugal at the Tokyo Olympics, held my country's record in both and I coach adult swimmers now."*
- *"I forgot swimming is the best exercise. I was a star swimmer from 6–18. Left high school with 7 school records, competed at nationals junior and senior year etc."*

### Receiving_Advice
The post asks for help on how to improve technique or overall swimming ability. Can include narration to give context for the question, or just be a single sentence with a question mark.

**Examples:**
- *"Of course I know the general motion, you can tell that just from seeing others swim, but I feel like I'd get in the water for the first time just to find out I basically can't swim anymore. I don't know if muscle memory will save me orrr... Has anyone been in a similar situation?"*
- *"Does anyone have any ideas for helping a kid understand how to move his body faster?"*

### Recommendations
The post asks for help on anything other than actual technique — can be problems while swimming or any general questions.

**Examples:**
- *"How to prevent water from going in nose without a plug? Nothing has really worked."*
- *"Best stretches to improve shoulder mobility? My dolphin kicking is horrible due to poor flexibility."*

### Update
The post gives a headline about recent news, events, or personal happenings. Evidence in the form of a link, citation, or paraphrase is used to inform the channel about the result of a recent competition or any other swimming-related news.

**Examples:**
- *"Kate Douglass breaks Sarah Sjöström's world record in 50 free"* — [swimswam.com](https://swimswam.com/kate-douglass-breaks-sarah-sjostroms-world-record-with-23-59-50-free/)
- *"I came across this article in Popular Mechanics the other day, Water Alters Your Consciousness, Research Suggests — And Can Induce a Trance-Like State"* — [archive.ph](https://archive.ph/i3Hu3)

---

## Data Collection Plan

Examples were collected from r/swimming, targeting approximately 50 examples per label for a balanced dataset of ~200 total. If any label was underrepresented after 200 examples, additional examples from that label were added to maintain balance.

### Label Distribution

| Label | Count |
|---|---|
| Receiving_Advice | 87 |
| Update | 49 |
| Advice | 36 |
| Recommendations | 28 |
| **Total** | **200** |

---

## Difficult-to-Label Examples

| Post Title | Assigned Label | Notes |
|---|---|---|
| *"I broke the 100m free WR??!"* | Update | Satirical post sharing an image of a time; intent is sharing a data artifact, not asking for help. Flagged as potentially satirical. |
| *"4 months into swimming: is 2:43/100m decent?"* | Update | Shares personal performance data (smartwatch image); asking "is this good?" is secondary to the data share. Compare with posts like *"I haven't swam in 8 years..."* which are purely seeking technique help. |
| *"Swam my first kilometer yesterday!"* | Advice | Primarily a milestone share with embedded questions at the end, but the post's purpose is sharing experience. |

---

## Fine-Tuning Approach

- **Base Model:** `distilbert-base-uncased`
- **Training Split:** 70% of 200 examples used for training
- **Metrics Reported:** Precision, Recall, Accuracy, F1 Score
- **Hyperparameter Decisions:** Epochs increased from 3 → 5; learning rate decreased from `2e-5` → `1e-5` to allow the model to learn more gradually and stably.

---

## Evaluation Report

### Overall Accuracy

| Model | Accuracy |
|---|---|
| Baseline | 0.667 |
| Fine-Tuned | 0.433 |

### Per-Class Metrics — Baseline Model

| Class | Precision | Recall | F1-Score | Support |
|---|---|---|---|---|
| Advice | 0.50 | 0.33 | 0.40 | 6 |
| Receiving_Advice | 0.62 | 1.00 | 0.76 | 13 |
| Recommendations | 1.00 | 0.50 | 0.67 | 4 |
| Update | 1.00 | 0.43 | 0.60 | 7 |
| **Accuracy** | | | **0.67** | **30** |
| Macro Avg | 0.78 | 0.57 | 0.61 | 30 |
| Weighted Avg | 0.73 | 0.67 | 0.64 | 30 |

### Per-Class Metrics — Fine-Tuned Model

| Class | Precision | Recall | F1-Score | Support |
|---|---|---|---|---|
| Advice | 0.00 | 0.00 | 0.00 | 6 |
| Receiving_Advice | 0.43 | 1.00 | 0.60 | 13 |
| Recommendations | 0.00 | 0.00 | 0.00 | 4 |
| Update | 0.00 | 0.00 | 0.00 | 7 |
| **Accuracy** | | | **0.43** | **30** |
| Macro Avg | 0.11 | 0.25 | 0.15 | 30 |
| Weighted Avg | 0.19 | 0.43 | 0.26 | 30 |

### Confusion Matrix — Fine-Tuned Model

| | Advice | Receiving_Advice | Recommendations | Update |
|---|---|---|---|---|
| **Advice** | 0 | 6 | 0 | 0 |
| **Receiving_Advice** | 0 | 13 | 0 | 0 |
| **Recommendations** | 0 | 4 | 0 | 0 |
| **Update** | 0 | 7 | 0 | 0 |

---

## Wrong Predictions (17 / 30)

### Example 1
| Field | Value |
|---|---|
| **Text** | *"Quick intro so you know why I'm writing this: I'm José. I swam distance freestyle for Portugal for about ten years, the 800 and 1500, with a stop at the Tokyo 2020 Olympics. Somewhere along the way..."* |
| **True Label** | Advice |
| **Predicted** | Receiving_Advice (confidence: 0.29) |
| **Reasoning** | The post starts with a first-person narrative, which the model likely interpreted as Receiving_Advice. Because Receiving_Advice had the most examples (87), the model learned to treat it as a "catch-all" label. |

### Example 2
| Field | Value |
|---|---|
| **Text** | *"Curious what's worked for people here because my shoulders are starting to feel permanently annoyed. Started swimming consistently again and forgot how quickly upper back/shoulder tightness sneaks up..."* |
| **True Label** | Recommendations |
| **Predicted** | Receiving_Advice (confidence: 0.29) |
| **Reasoning** | The distinction between Recommendations (non-technique advice) and Receiving_Advice (technique advice) was not learned, likely due to limited examples in the Recommendations class. |

### Example 3
| Field | Value |
|---|---|
| **Text** | *"I'm in month 3 of swimming and I'm addicted. I've tried two different methods while practicing front crawl. Method A: Continuing to breathe out all the way got me gasping for air in only 10–15 meters..."* |
| **True Label** | Advice |
| **Predicted** | Receiving_Advice (confidence: 0.32) |
| **Reasoning** | The model learned Receiving_Advice as a catch-all and defaults to it. More balanced examples and full-prompt reading would address this. |

---

## Sample Classifications

| # | Text (truncated) | True Label | Predicted | Confidence | Notes |
|---|---|---|---|---|---|
| 1 | *"I have been playing around with this, sometimes I look down at the bottom and sometimes I look ahead..."* | Receiving_Advice | Receiving_Advice ✅ | 0.30 | Reasonable — asks for suggestions about head/eye movement (technique). |
| 2 | *"Hii! I'm a swimmer from a small club and we did a long distance gala. We did as many lengths of a 25m pool as we could for an hour..."* | Receiving_Advice | Receiving_Advice ✅ | 0.31 | Reasonable — asks about time standards and overall swimming ability. |
| 3 | *"So it's coming into winter here in Australia and my local pool is outdoors. I currently swim 2x a week long swims..."* | Update | Receiving_Advice ❌ | 0.31 | Misclassified due to model's catch-all behavior. |
| 4 | *"I've been swimming regularly for about 8 months. My main issue is endurance. After 50 meters of freestyle, I usually need to stop..."* | Advice | Receiving_Advice ❌ | 0.31 | Misclassified; post is sharing advice from experience. |
| 5 | *"I saw this post last month about someone who started swimming at 33 and it changed their life for the better..."* | Update | Receiving_Advice ❌ | 0.30 | Misclassified; post is sharing an update/news item. |

---

## Reflection

The model severely overfit to the `Receiving_Advice` label, classifying every post into this category. The intended behavior was to distinguish between all four labels, but the class imbalance (87 Receiving_Advice vs. 28 Recommendations) caused the model to treat `Receiving_Advice` as a catch-all. To fix this, the dataset would need more balanced class representation, particularly more examples for `Advice` and `Recommendations`.

---

## Spec Reflection

The spec helped track each step of the process and clarify what each section of the notebook would be used for. The planning section at the beginning enabled useful brainstorming and helped identify a community that fit the project's scope.

One divergence from the spec: the number of epochs was increased (3 → 5) and the learning rate was decreased (`2e-5` → `1e-5`) after the initial run produced very low accuracy. These changes did improve results, though the overall fine-tuned model still underperformed the baseline.

---

## AI Usage

- **Labelling:** Claude was used to assist in labelling approximately half of the examples, following the label definitions and edge-case guidelines provided.
- **Error Analysis:** Claude was asked to explain why the model consistently predicted `Receiving_Advice`. It identified the likely cause as a small and imbalanced dataset rather than a labelling problem.
- **Debugging:** Gemini was used to fix runtime errors in the notebook. It added import statements (which were reviewed and verified). Gemini also added an F1 score metric directly in the code alongside the existing accuracy measure.
