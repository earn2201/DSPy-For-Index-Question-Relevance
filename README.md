# DSPy Optimization for Market Question Relevance

This repository demonstrates how to use **DSPy** to automatically optimize prompt-based reasoning for a structured classification and scoring task. Specifically, the notebook shows how to generate a **relevance score, rationale, and binary label** that evaluate how well a given *prediction market question* predicts or relates to a broader *index question*.

The project uses DSPy’s **BootstrapFewShotWithRandomSearch** optimizer and **Chain-of-Thought** reasoning to automate prompt selection and improve performance using a small, curated dataset.

---

## Problem Overview

Given:
- An **index question** (e.g., *"Will the next US national election favor the democratic party?"*)
- A **market question** (e.g., *"Will JD Vance win the 2028 presidential election?"*)

The goal is to predict:
- **label**: whether the market question is relevant (`1`) or not (`0`)
- **score**: a continuous relevance score in `[0, 1]`
- **rationale**: a short natural-language explanation justifying the decision

---

## Dataset

- **72 labeled examples**
- Each example includes:
  - `index_question`
  - `market_title`
  - `rationale`
  - `label` (binary relevance)
  - `score` (graded relevance)

Examples span multiple domains, including:
- Space and science
- Economics and markets
- Culture and media
- Public policy and social metrics

The dataset includes:
- **Directly predictive** relationships
- **Partially predictive** relationships
- **Clearly unrelated** pairs

---

## Approach

### DSPy Programs

This notebook defines a DSPy **ChainOfThought** program that maps:

(index_question, market_title) → (rationale, label, score)


Chain-of-thought reasoning is used to encourage structured and explainable outputs.

---

### Optimization Strategy

Prompt engineering is automated using:

**BootstrapFewShotWithRandomSearch**

This optimizer:
- Samples candidate few-shot prompt configurations
- Evaluates them against a validation set
- Selects the configuration that maximizes a user-defined metric

The optimizer compiles the high-level DSPy program into an optimized prompt that is reused consistently for inference.

---

## Experimental Setup

- **Training set:** 30 examples  
- **Validation set:** 42 examples  
- **Model:** `gpt-4.1-mini` (OpenAI)  
- **Temperature:** 0  
- **Top-p:** 1  
- **Random seeds:** Fixed for full reproducibility  
