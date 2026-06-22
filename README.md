Wrong predictions: 14 / 30

--- #1 ---
Text:      I can not fucking believe the amount of rapey reviews I've been reading on here: people wanting the One Wish Willow sticks to do the same thing to their crush. Nikki has NO FREE WILL. She did not cons...
True:      personal_reaction
Predicted: low_effort_quip  (confidence: 0.35)

--- #2 ---
Text:      Had an alright time watching this. Sometimes you go to a movie and you just watch the story. Weird that he didn't try to get out of there immediately after she cooked and served him his own dead cat. ...
True:      personal_reaction
Predicted: low_effort_quip  (confidence: 0.36)

--- #3 ---
Text:      the real horror is male entitlement and nice guy syndrome.
True:      personal_reaction
Predicted: low_effort_quip  (confidence: 0.37)

--- #4 ---
Text:      I'LL RIP MY EYES OUT OF MY FUCKING SKULL AND SHOVE THE BARREL UP MY PUSSY BITCHHHHHHH
True:      personal_reaction
Predicted: low_effort_quip  (confidence: 0.36)

--- #5 ---
Text:      go ahead and start engraving inde navarrette on the oscar
True:      cinematic_critique
Predicted: low_effort_quip  (confidence: 0.38)

--- #6 ---
Text:      the last ten minutes nearly sent me into cardiac arrest
True:      personal_reaction
Predicted: low_effort_quip  (confidence: 0.38)

--- #7 ---
Text:      Further proof that when a guy gets friend zoned it's actually the girl that suffers most
True:      personal_reaction
Predicted: low_effort_quip  (confidence: 0.37)

--- #8 ---
Text:      YOU CAN'T USE CURRENT JOYS LIKE THAT BRO
True:      personal_reaction
Predicted: low_effort_quip  (confidence: 0.39)

--- #9 ---
Text:      man or Bear? actually fck that what's the secret third option 🫪. rewatched this in a PACKED theater, 10/10 experience to hear the crowd's reaction to the scenes i knew were coming! THINGS I NOTICED ON...
True:      cinematic_critique
Predicted: low_effort_quip  (confidence: 0.34)

--- #10 ---
Text:      We live in horror societies built on horror relationships, yet paradoxically, too often the genre that should tell this horror story escapes from reality and retreats into the supernatural. It's good ...
True:      cinematic_critique
Predicted: low_effort_quip  (confidence: 0.35)

--- #11 ---
Text:      I'd just wish for my cat to be alive again, maybe that's just me.
True:      personal_reaction
Predicted: low_effort_quip  (confidence: 0.38)

--- #12 ---
Text:      this was actually so fucking scary?? i had to drive an hour home after seeing this at like 1am and i swear i was so paranoid, i kept seeing nikki on the side of the road. this freaked me out so bad, b...
True:      personal_reaction
Predicted: low_effort_quip  (confidence: 0.36)

--- #13 ---
Text:      Really brilliant addition to the snapping a stick goes wrong cinematic universe. It's always exciting to see a new voice pop onto the scene fully formed, and man sometimes I forget how much of a treat...
True:      cinematic_critique
Predicted: low_effort_quip  (confidence: 0.34)

--- #14 ---
Text:      Inde navarrette i see your future and its very bright that's a performance of a lifetime!
True:      cinematic_critique
Predicted: low_effort_quip  (confidence: 0.36)



# TakeMeter: Letterboxd Discourse Classifier for *Obsession* (2026)

TakeMeter is a custom machine learning pipeline designed to classify user reviews from the Letterboxd community for the 2026 horror/thriller release *Obsession*. It evaluates and categorizes the highly unstructured, slang-heavy, and chaotic nature of modern social movie discourse into three distinct categories: structural film critiques, immediate visceral reactions, and low-effort jokes/memes.

This project contrasts a zero-shot Large Language Model baseline (**Llama 3.3 via Groq**) against a small, locally fine-tuned transformer model (**DistilBERT**).

---

## 1. Community Choice & Reasoning

* **Target Community:** Letterboxd public reviews for the film *Obsession*.
* **Reasoning:** Letterboxd is an ideal environment for a text classification task due to its highly varied, democratic discourse styles. Unlike traditional professional film review aggregates, its users do not adhere to formal templates. On any given movie page, dense film-school critiques of cinematography and acting live directly alongside chaotic raw updates ("crying in the theater") and highly upvoted, ironic, one-liner internet memes. This structural collision of analytical craft, personal raw feeling, and meme-driven shitposting provides a challenging, non-trivial landscape for testing text classification boundaries.

---

## 2. Label Taxonomy

Our system categorizes all incoming reviews into one of three primary intent-based classes:

### `low_effort_quip`
* **Definition:** One-liners, pop-culture memes, or Letterboxd-specific inside jokes meant to be punchy and funny, requiring low analytical effort.
* **Examples:**
  1. *"one man has a crush and makes it everyone's problem"*
  2. *"Male loneliness final boss"*

### `personal_reaction`
* **Definition:** Captures the viewer's immediate subjective, real-world experience, gut feelings, physiological states (crying, shaking, nausea), theater environment, or personal memories.
* **Examples:**
  1. *"Jesus… i’m still shaking! That was fucking exhilarating."*
  2. *"the last ten minutes nearly sent me into cardiac arrest"*

### `cinematic_critique`
* **Definition:** Evaluates the technical components of filmmaking, including cinematography, acting, directing, editing, screenplay, pacing, or score.
* **Examples:**
  1. *"Inde navarrette i see your future and its very bright that's a performance of a lifetime!"*
  2. *"absolutely nothing can prepare you for inde navarrette's performance"*

---

## 3. Data Collection, Distribution & Annotation

### Data Profile
* **Source:** Scraping and manual aggregation of public user review data from Letterboxd for the movie *Obsession*.
* **Dataset Size:** ~200 rows.
* **Test Set Size:** 30 samples.
* **Label Distribution (Test Set):**
  * `low_effort_quip`: 12 samples (40%)
  * `personal_reaction`: 9 samples (30%)
  * `cinematic_critique`: 9 samples (30%)

### Difficult Annotation Examples & Tie-Breaker Decisions
When reviews blurred boundaries, we implemented a hard **Primary Intent Tie-Breaker** rule: *"Why did the user choose to write this comment?"*

1. **Text:** *"we all had that one relationship 😂😂😂😂😂😂😂😂😂😂😂😂😂😂😂"*
   * *Conflict:* Blurs personal nostalgia with a joke format.
   * *Decision:* **`low_effort_quip`**. The extreme overuse of emojis and generic phrasing shifts the weight from shared personal depth to a low-effort relatability meme.
2. **Text:** *"I'm suddenly very ok with being single"*
   * *Conflict:* Blurs a humorous relationship joke with an emotional response to a scary film.
   * *Decision:* **`personal_reaction`**. The core intent represents a immediate personal sense of relief and a gut-level reaction to the toxic relationship dynamics on display.
3. **Text:** *"go ahead and start engraving inde navarrette on the oscar"*
   * *Conflict:* Blurs an ironic pop-culture hyperbole format with an appreciation of acting.
   * *Decision:* **`cinematic_critique`**. Despite using casual internet slang formatting, the primary driver for writing the post is to evaluate and praise the lead actress’s performance.

---

## 4. Baseline Description

* **Model Used:** `llama-3.3-70b-versatile` (via Groq).
* **Setup:** Evaluated using zero-shot prompt testing. The model was given a system prompt containing our exact community task description, one-sentence class criteria definitions, single exemplar post structures, and a strict instructions boundary to output *only* the raw valid label string.
* **Prompt Used:**
```text
You are classifying user reviews from the Letterboxd community for the movie 'Obsession'.
Assign each post to exactly one of the following categories based on the user's primary intent.

low_effort_quip: One-liners, pop-culture memes, or Letterboxd-specific jokes meant to be punchy, funny, and require low analytical effort.
Example: "one man has a crush and makes it everyone's problem"

personal_reaction: Captures the viewer's immediate subjective, real-world experience, gut feelings, physiological states (crying, shaking, nausea), theater environment, or personal memories.
Example: "Jesus… i’m still shaking! That was fucking exhilarating."

cinematic_critique: Evaluates the technical components of filmmaking, including cinematography, acting, directing, editing, screenplay, pacing, or score.
Example: "absolutely nothing can prepare you for inde navarrette's performance"

Respond with ONLY the label name.
Do not explain your reasoning.
```

## 5. Fine-Tuning Approach

* **Base Model:** `distilbert-base-uncased` (via Hugging Face).
* **Training Setup:** Trained on a Google Colab T4 GPU platform utilizing `transformers.Trainer`.
* **Hyperparameter Strategy:**
  * **Epochs:** 3
  * **Batch Size:** 16

## 6. Full Evaluation Report

### Performance Metrics Comparison

| Model | Test Accuracy | Macro F1-Score | Result Status |
| :--- | :--- | :--- | :--- |
| **Zero-Shot Baseline (Groq/Llama 3.3)** | 66.7% (0.6667) | 0.65 | Nearing the target success boundaries of 75%. |
| **Fine-Tuned DistilBERT** | 53.3% (0.5333) | 0.42 | Regression (-13.3%) due to class collapse. |

### Detailed Classification Breakdown

Zero-Shot Baseline (Groq):
                    precision    recall  f1-score   support

   low_effort_quip       0.77      0.83      0.80        12
 personal_reaction       0.50      0.44      0.47         9
cinematic_critique       0.67      0.67      0.67         9

Fine-Tuned DistilBERT:
                    precision    recall  f1-score   support

   low_effort_quip       0.46      1.00      0.63        12
 personal_reaction       0.00      0.00      0.00         9
cinematic_critique       1.00      0.44      0.62         9

Baseline Error Reflection
Where it struggled: The baseline heavily struggled with personal_reaction (hitting a weak 0.47 F1-score with a 0.44 recall). It missed more than half of the true emotional reactions in the test set.

What it confuses: It consistently confuses emotional hyperbole with jokes.

Hypothesis: Because Letterboxd users express raw emotional states using extreme internet exaggeration (e.g., "sent me into cardiac arrest" or "I nearly shit myself"), the zero-shot baseline treats these text patterns as literal jokes and misclassifies them as low_effort_quip.

### Fine-Tuned Model Confusion Matrix

The fine-tuned DistilBERT collapsed heavily into the majority class (`low_effort_quip`), completely erasing its capability to isolate `personal_reaction` boundaries.

| Actual \ Predicted | low_effort_quip | personal_reaction | cinematic_critique |
| :--- | :---: | :---: | :---: |
| **low_effort_quip** | 12 | 0 | 0 |
| **personal_reaction** | 9 | 0 | 0 |
| **cinematic_critique** | 5 | 0 | 4 |

---

### Deep-Dive Failure Analysis (3 Specific Examples)

The fine-tuned model yielded 14 / 30 wrong predictions. Three highly indicative examples expose its core operational gaps:

#### ❌ Error 1: Visceral Hyperbole Misread as a Joke
* **Text:** `"the last ten minutes nearly sent me into cardiac arrest"`
* **True Label:** `personal_reaction`
* **Predicted Label:** `low_effort_quip` (Confidence: 0.38)
* **Analysis:** Letterboxd users consistently use intense physical exaggerations ("cardiac arrest") to highlight emotional shock. Because the training set was too small to contextualize these idioms, DistilBERT read the short, punchy sentence structure as an internet meme rather than a visceral reaction statement.

#### ❌ Error 2: Missing the Context of Social Commentary
* **Text:** `"I'LL RIP MY EYES OUT OF MY FUCKING SKULL AND SHOVE THE BARREL UP MY PUSSY BITCHHHHHHH"`
* **True Label:** `personal_reaction`
* **Predicted Label:** `low_effort_quip` (Confidence: 0.37)
* **Analysis:** This comment features an all-caps, exclaimation showing that the user is excited, frustrated, anger, in a comedic way. The focus is on how absurd of a comment
it is which places emphasis on the reaction the user has, and not on the comedic element or the specifics of what they are saying.

#### ❌ Error 3: Praise of Acting Craft Overruled by Syntax Traps
* **Text:** `"go ahead and start engraving inde navarrette on the oscar"`
* **True Label:** `cinematic_critique`
* **Predicted Label:** `low_effort_quip` (Confidence: 0.38)
* **Analysis:** This review is an evaluation of an acting performance. However, because it leads with a conversational phrase ("go ahead and start..."), DistilBERT defaulted to classifying it as a low-effort joke format with a weak confidence split (~34% to 38%).

---

### Sample Classifications

| Review Text | Predicted Label | Confidence | Status |
| :--- | :--- | :---: | :---: |
| *"Really brilliant addition to the snapping a stick goes wrong cinematic universe..."* | `low_effort_quip` | 0.34 | Incorrect |
| *"the last ten minutes nearly sent me into cardiac arrest"* | `low_effort_quip` | 0.38 | Incorrect |
| *"one man has a crush and makes it everyone's problem"* | `low_effort_quip` | 0.39 |  Correct |

> **Validation of Correct Sample:** The phrase *"one man has a crush and makes it everyone's problem"* maps perfectly to a short, modern joke format. Since our model collapsed into choosing `low_effort_quip` for nearly every low-confidence sample, it naturally hit this standard quip perfectly. The model defaulted to low_effort_quip across all three samples because they all share a short, casual internet syntax which was a reasonable guess for the model, although it was not ultimately correct.

---

## 7. Project Reflection

### What the Model Learned vs. What We Intended
We wanted a model that understands the actual *intent* behind a review, but our fine-tuned DistilBERT took a shortcut instead. Because our dataset was tiny (~200 reviews) and trained for only 3 epochs, the model simply looked at text length and casual phrasing, defaulting to the most common label (`low_effort_quip`) while completely missing key context words like "performance" or "oscar."

To fix this next time, we need to:
* Expand the dataset to over 1,000 balanced rows to use more sample data.
* Train for 8–10 epochs at a higher learning rate (3e-5) to break the model out of its lazy guessing habits according to Gemini.

### Specification & Workflow Reflection
* **How the spec helped:** Forcing ourselves to write clear definitions and edge cases in `planning.md` made it incredibly easy to spot exactly *why* and *where* the model was failing during testing.
* **Where we diverged:** We assumed a fine-tuned model would easily beat a general LLM. Instead, we learned that zero-shot LLMs have a massive advantage on social media 
and other data because they already understand internet slang, pop culture, and casual idioms right out of the box.

## 8. AI Tool Usage Documentation

### Instance 1: Formatting and Structural Cleanup
* **Direction:** Gave Gemini our raw ideas and taxonomy definitions.
* **Production:** Generated the clean Markdown layout for our tables.
* **Override:** Manually rewrote several generic AI definitions to fit the actual patterns we saw in our Letterboxd data. Replaced some incorrect explanations.

### Instance 2: Failure Analysis Diagnostics
* **Direction:** Fed Gemini reviews for them to be pre-labeled.
* **Production:** A number of reviews were given labeles that were off. Occasionally Gemini and/or Claude would fail to recognize the subtly of sarcasm in a funny comment
and label it a personal_reaction or another incorrect label.
* **Override:** Conducted a manual audit of all 200 rows, overriding flawed AI labels to force label consistency.