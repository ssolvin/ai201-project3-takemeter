# Project Plan: TakeMeter (Obsession Review Discourse Classifier)

## 1. Community Choice
* **Community:** Letterboxd (specifically tracking public user reviews for the 2026 horror/thriller release *Obsession*).
* **Why this community?** Letterboxd is an ideal environment for a text classification task because its discourse is incredibly varied. Unlike traditional academic film sites, its users do not adhere to a single review template. On any given film page, dense film-school critiques of cinematography and acting live directly alongside real emotional updates ("crying in the theater") and highly upvoted, ironic, one-liner comments. This collision of structural craft analysis, personal raw feeling, and meme-driven shitposting provides a rich landscape for testing the boundaries of a text classifier.

---

## 2. Label Taxonomy

### 1. `low_effort_quip`
* **Definition:** One-liners, pop-culture memes, or Letterboxd-specific jokes meant to be punchy, funny, and require low analytical effort.
* **Core Question:** Is the post primarily written as a joke to gain quick engagement or likes?
* **Examples:**
  * *"one man has a crush and makes it everyone's problem"*
  * *"Male loneliness final boss"*
* **Uncertain Case & Rule:** *"we all had that one relationship 😂😂😂😂😂😂😂😂😂😂😂😂😂😂😂"* 
  * *Boundary:* This is uncertain, because it's a comment that is meant to be funny and relatable, but it could also possibly fall under personal reaction. The number of emojis
and relatability could play into the user stating that the movie reminded them of one of their past relationships and the emoji is them laughing at that fact. I
classified it as low effort quip, because the purpose of the comment places more emphasis on being funny, than their own personal reaction.

### 2. `personal_reaction`
* **Definition:** Captures the viewer's immediate subjective, real-world experience, gut feelings, physiological states (crying, shaking, nausea), theater environment, or personal memories.
* **Core Question:** Does it focus on how the movie made the specific viewer feel or react in the room?
* **Examples:**
  * *"Jesus… i’m still shaking! That was fucking exhilarating."*
  * *"the last ten minutes nearly sent me into cardiac arrest"*
* **Uncertain Case & Rule:** *"I'm suddenly very ok with being single"*
  * *Boundary:* This is an uncertain case, because the comment is a personal reaction to the movie. The user is glad that they are single
after seeing the scary and intense relationship in the movie. This comment is also meant to be funny, phrasing their reaction as a sudden feeling of relief for what
most people consider a good thing: relationship. Because the primary focus is on their own reaction, it is labeled as a personal reaction.

### 3. `cinematic_critique`
* **Definition:** Evaluates the technical components of filmmaking, including cinematography, acting, directing, editing, screenplay, pacing, or score.
* **Core Question:** Does it evaluate how the movie was structurally or artistically constructed?
* **Examples:**
  * *"Inde navarrette i see your future and its very bright that's a performance of a lifetime!"*
  * *"absolutely nothing can prepare you for inde navarrette's performance"*
* **Uncertain Case & Rule:** *"go ahead and start engraving inde navarrette on the oscar"*
  * *Boundary:* This is an uncertain example, because while the main focus of the comment is to praise the lead actress, it's also funny meanting that the actress should already have her name engraved on an oscar for her amazing performance. Because it is primarily praising the actress, it is considered a cinematic critique rather than a low effort quip.

---

## 3. Hard Edge Cases
If we encounter edge cases that make it difficult to determine what label should be given, focus entirely on the main idea and primary intent of the comment.
Ask yourself: "Why did the user write this?"

---

## 4. Data Collection Plan
* **Source:** Publicly available user reviews for *Obsession* on Letterboxd. 
* **Target Count:** The target is a minimum of 200 examples.
* **Target Distribution:** We will aim for a relatively uniform distribution across categories, ensuring no single class represents more than 50% of the data and a minimum of
20% per label.
* **Handling Imbalance:** If any label is heavily underrepresented (falling below 20% of the dataset) after collecting 200 entries, we will perform targeted data collection by specifically searching out longer, paragraph-form reviews to boost `cinematic_critique`, or shortest reviews to boost `low_effort_quip` until a healthy balance is maintained.

---

## 5. Evaluation Metrics
We will evaluate both the zero-shot baseline (`llama-3.3-70b-versatile`) and our fine-tuned `distilbert-base-uncased` model using the following metrics:

* **Overall Accuracy:** To track the total percentage of correct classifications across the entire locked test set.
* **Per-Class F1-Score:** Because Letterboxd comments can be short and highly subjective, accuracy alone is insufficient. We need to look at Precision (out of all posts the model predicted as a joke, how many actually were jokes?) and Recall (how many of the total jokes did the model successfully catch?). The **F1-Score** is the mean of these two, which will reveal if the model is over-predicting a dominant class or failing entirely on a specific fuzzy boundary (such as distinguishing quips from personal reactions).

---

## 6. Definition of Success
* **Deployment Threshold:** For this classifier to be genuinely useful as a community filtering tool (e.g., allowing a Letterboxd user to filter out memes and read only technical critiques), the model must hit a **minimum overall accuracy of 75%**.
* **Success Criteria:** Furthermore, the `cinematic_critique` class must achieve an **F1-score of >= 0.75**. Because filtering out noise to find deep analysis is the core utility of such a tool, the model cannot succeed merely by guessing the majority meme class correctly; it must accurately isolate true craft critiques. 


---

## 7. AI Tool Plan

### 1. Label Stress-Testing
We will ask ChatGPT/Claude to generate 10 tricky, borderline reviews that sit between our labels. If we cannot easily classify the AI’s examples using our current definitions, we will sharpen our rules before finalizing the data.

### 2. Annotation Assistance
While obsession_reviews.csv is already manually labeled, if we use an LLM to pre-label any extra reviews to reach our 200-item goal, we will manually check and correct every single AI prediction line-by-line. Any AI assistance will be fully disclosed in the final report.

### 3. Failure Analysis
After training, we will feed all of the model's incorrect test predictions into an LLM to help find common error patterns (like the model consistently messing up sarcasm, short comments, or specific label pairs). We will then manually verify these patterns ourselves.

#### 4. Planning.md
I brainstormed and answered the core design questions myself to establish the community focus, label boundaries, and success thresholds. I then used Gemini to beautify the formatting, clean up the phrasing of the edge cases, and ensure the planning document was readable and clear.

#### 5. Data Collection
I will use a mix of manual input gathering, but will utilize Gemini and Claude to help me format the CSV file and pre-label the comments/content. After being labeled, I
manually check each example and correct labels that I believe are incorrect and also note which ones may be off.