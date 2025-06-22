README.txt (For understanding the code)

---

# Natural Language Queries in Egocentric Videos (Ego4D - NLQ Benchmark)

##  Project Goal

This project focuses on solving the **Natural Language Queries (NLQ)** task from the Ego4D dataset. The aim is to predict the relevant video segment for a given natural language query. For instance, a query like *“Where did I put the mug?”* must be answered by locating the start and end times within the egocentric video where this event occurs.

---

## Project Structure

The codebase is organized into multiple components, including baseline implementations, dataset preparation, and one extension. Here's a breakdown:

##Analysis### Before diving into model development, we conducted an initial analysis of the Ego4D Natural Language Queries (NLQ) dataset as requested to better understand its structure and content. This included exploring the distribution of query templates to identify common linguistic patterns, analyzing the average duration of annotated clips along with their corresponding query and answer temporal segments, and examining how queries are distributed across various scenarios in the dataset. These exploratory steps, supported by visual plots, helped us gain valuable insights into the dataset’s characteristics and informed several design choices in the later stages of our project. 


### Model Implementations
We implemented and trained two models:
- `VSLBase`: A baseline model using GloVe embeddings.
- `VSLNet`: An enhanced version that includes a **Query-Guided Highlighting** mechanism.

**NOTE** While working with vslbase, we changed three files to convert it to vslbase (runner, main,vslnet) All three files we have uploaded in the directory, so while working with runtime, you need to change the three while to run your code with vslbase 

Each model was trained using two different features:
- **Omnivore features** (official Ego4D pre-extracted)
- **EgoVLP features**

So, in total, there are **6 different scripts** representing:
1. Omnivore + VSLBase  
2. Omnivore + VSLNet  
3. Omnivore + GloVe  
4. EgoVLP + VSLBase  
5. EgoVLP + VSLNet  
6. EgoVLP + GloVe

**Note:** Although these six scripts may appear similar, they differ in configuration, models used, and feature inputs. They also correspond to the **first two project steps** (before the extension and baseline comparisons).  
> Some scripts save output files at the end (e.g., predictions and scores), while others don’t — **but all results are best understood by reading the final project report**, where everything is clearly described and compared.

---
##  Training & Evaluation of models.

- Training was conducted using pre-extracted features (Omnivore & EgoVLP).
- Models used either **GloVe embeddings** or **BERT** for queries.
- Loss includes standard localization loss and a highlight loss (weighted).
- Metrics: **Recall@K** and **mIoU (mean Intersection over Union)**.
- Checkpoints were saved and evaluated periodically.

---

### Extension Implementation


- One file contains the **full implementation of Extension 2**:  
  “From video interval to a textual answer.”

This script includes:
- Segment selection
- Manual annotation of answers
- Video segment extraction (via `ffmpeg`)
- Inference using a VideoQA model (e.g., Video-LLaVA)
- Result generation and qualitative+quantitative analysis
- We have seen the result with some quantitative metrics (e.g. ROUGE or BLEU)

The code is well-commented and step-by-step, making it easy to replicate the extension.

---



### Additional Resources

- A **ZIP file** is included with:
  - Results and predictions
  - The 50 queries selected for Extension 2
  - Final matched answers used for evaluation

---



---

##  Final Note

For a complete understanding of the pipeline, experimental setup, and results:
> ** Please refer to the final written report.**

It provides:
- Model comparisons
- Config differences across the 6 runs
- We used the graphs to compare the results (mentioned in the report)
- Explanation of how we finalized query-answer pairs
- The model we used is mentioned in the report, but can also be checked in the extension2 file 
