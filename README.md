# Spotify Customer Support AI Triage Agent

An automated customer support triage system powered by Google Gemini to classify incoming user queries, route issues, and generate response drafts.

---

## Executive Summary

* **Intent Classification Accuracy**: **82.00%** (outperforms keyword baseline by +40.50%)
* **Action Routing Accuracy**: **96.50%** (reliable identification of issues requiring human escalation)
* **Dataset**: Evaluated on $N = 200$ customer support interactions with golden ground-truth labels.

---

## Benchmark Results

| Approach | Intent Accuracy | Action Routing Accuracy | Key Characteristics |
| :--- | :---: | :---: | :--- |
| **Majority Baseline** | 20.00% | 50.00% | Always predicts the most common class |
| **Keyword Rule Baseline** | 41.50% | 68.00% | Simple string matching rules |
| **Gemini Triage Agent** | **82.00%** | **96.50%** | Context-aware zero-shot LLM pipeline |

---

## System Architecture

The pipeline processes raw incoming queries through three automated stages:

1. **Intent Categorization**: Assigns one of five granular intents (`ACCOUNT_ACCESS`, `BILLING_SUBSCRIPTION`, `TECHNICAL_ISSUE`, `FEATURE_REQUEST`, or `GENERAL_FEEDBACK`).
2. **Action Determination**:
   * `AUTO_HANDLE`: How-to steps, clear FAQ queries, and standard troubleshooting.
   * `ESCALATE`: Payment failures, unauthorized charges, account compromise, or high-frustration cases.
3. **Response Drafting**: Generates context-specific, professional customer support responses ready for delivery or human review.

---

## Failure Analysis & Engineering Insights

* **Cross-Domain Ambiguity**: Tweets that combine a software bug with an immediate billing threat (e.g., *"App crashes every time I try to cancel my subscription"*) represent the majority of intent misclassifications.
* **Escalation Safety Bias**: The model prioritizes human escalation over automation whenever sentiment is strongly negative, favoring customer retention over aggressive automation.
* **Short-Context Queries**: Tweets under five words lack sufficient semantic tokens, occasionally defaulting to general feedback.

---

## Repository Contents

* `Yet_another_copy_of_Hiver_SDE_Assinment (1).ipynb` — Complete pipeline execution, baseline comparisons, and evaluation charts.
* `golden_eval_final_results (2).csv` — Verified predictions, intent classifications, action routings, and generated response drafts.
* `README.md` — Project architecture, benchmarks, and failure analysis documentation.
*
