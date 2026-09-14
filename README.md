# Spotify Customer Support AI Triage Agent

An automated customer support triage system powered by Google Gemini to classify incoming user queries, route issues, and generate response drafts.

---

## Executive Summary

* **Intent Classification Accuracy**: **82.00%**
* **Action Routing Accuracy**: **96.50%**
* **Dataset**: Evaluated on **N = 200** manually labelled customer support interactions.
* **LLM-as-a-Judge Pass Rate**: **95.5%**

---

## Benchmark Results

| Approach | Intent Accuracy | Intent Macro F1 | Action Accuracy | Action Macro F1 |
| :--- | :---: | :---: | :---: | :---: |
| **Trivial Baseline** | 42.50% | 0.119 | 76.50% | 0.433 |
| **Simple Baseline** | 70.00% | 0.658 | 87.00% | 0.833 |
| **Proposed Gemini Agent** | **82.00%** | **0.773** | **96.50%** | **0.949** |

### Key Findings

The Proposed Gemini Agent achieved the best performance across both intent classification and triage-action prediction.

Compared with the Simple Baseline:

* Intent Accuracy improved by **12.0 percentage points**
* Intent Macro F1 improved by **0.115**
* Action Accuracy improved by **9.5 percentage points**
* Action Macro F1 improved by **0.116**

---

## System Architecture

The pipeline processes raw incoming customer queries through three automated stages:

1. **Intent Categorization**
   * Assigns each query to one of five support intents.

2. **Action Determination**
   * `AUTO_HANDLE`: Clear FAQ queries, how-to requests, and standard troubleshooting.
   * `ESCALATE`: Payment failures, unauthorized charges, account compromise, or cases requiring human investigation.

3. **Response Drafting**
   * Generates a context-specific, professional Spotify-style response ready for delivery or human review.

---

## Evaluation

The system was evaluated using a **200-example golden evaluation set**.

Evaluation included:

* Intent Accuracy
* Intent Macro F1
* Action Accuracy
* Action Macro F1
* LLM-as-a-Judge evaluation
* Human agreement analysis

Human agreement results:

* **Intent Cohen's Kappa: 0.812**
* **Action Cohen's Kappa: 0.894**

---

## Failure Analysis & Engineering Insights

### 1. Cross-Domain Ambiguity

Some tweets combine multiple support problems, such as a technical issue occurring during subscription cancellation.

**Example:**  
*"App crashes every time I try to cancel my subscription."*

**Hypothesis:** The model must choose one primary intent when a single message contains multiple issue types.

### 2. Escalation Safety Bias

The model sometimes prefers human escalation when the customer expresses strong frustration, even when the underlying issue could potentially be handled automatically.

**Hypothesis:** Strong negative sentiment can influence the model toward safer escalation.

### 3. Short-Context Queries

Very short tweets can lack enough information for reliable intent classification.

**Example:**  
*"Still not working."*

**Hypothesis:** Additional conversation context or historical customer messages would improve classification.

---

## Reproducibility

The complete pipeline is provided in the Jupyter/Colab notebook.

The notebook includes:

1. Dataset loading and preprocessing
2. Spotify customer-support conversation pairing
3. Golden-set sampling and manual labelling
4. Trivial baseline
5. Keyword-rule baseline
6. Gemini triage agent
7. Automated evaluation metrics
8. LLM-as-a-Judge evaluation
9. Human agreement analysis
10. Failure analysis

The evaluation uses **200 golden examples**.

---

## Repository Contents

* `Yet_another_copy_of_Hiver_SDE_Assinment (1).ipynb` — Complete pipeline execution, baseline comparisons, and evaluation.
* `golden_eval_final_results (2).csv` — Golden evaluation predictions, intent classifications, action routings, and generated response drafts.
* `README.md` — Project architecture, benchmarks, evaluation methodology, and failure analysis.

---

## One-Week Improvement Plan

With one additional week, the highest-impact improvements would be:

1. Add conversation-history context instead of classifying isolated tweets.
2. Improve multi-intent detection for messages containing billing + technical issues.
3. Add confidence scoring and threshold-based escalation.
4. Expand the golden evaluation set beyond 200 examples.
5. Test additional prompting strategies and models.

---

## Key Engineering Decisions

* Used a small, manually defined intent taxonomy to keep classification actionable.
* Established trivial and keyword baselines before evaluating the LLM.
* Used a manually labelled golden evaluation set rather than relying only on automated labels.
* Separated intent classification from action routing.
* Added human escalation for sensitive or high-risk cases.
* Evaluated both classification quality and operational routing quality.
* Used LLM-as-a-Judge to evaluate generated response quality.
* Measured human agreement using Cohen's Kappa.
