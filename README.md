<h1 align="center">📩 SMS Spam Classifier</h1>
<p align="center">
  <img src="https://i.imgur.com/uCbB9nD.gif" alt="Spam Detection Demo" width="400"/>
</p>

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.8.0-orange?logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Model: BernoulliNB](https://img.shields.io/badge/Model-BernoulliNB-purple)](https://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.BernoulliNB.html)

A lightweight, production-ready Email/SMS spam detection system built with a **Bernoulli Naive Bayes** classifier. Trained on the [Spam Email Classification Dataset](https://www.kaggle.com/datasets/phangud/spamcsv), the model distinguishes ham (legitimate) messages from spam with a vocabulary of **6,715 features**.

---



## Overview

This project packages a trained spam classifier as a single serialized `model_bundle.pkl` file containing the fitted vectorizer and the Naive Bayes model. This design means zero preprocessing steps at inference time — just load and predict.

**Key characteristics:**
- Binary classification: `0 = ham`, `1 = spam`
- Class distribution: ~87.6% ham / 12.4% spam (reflects real-world SMS imbalance)
- Vocabulary: 6,715 unigram features extracted from SMS text
- Laplace smoothing (α = 1.0) for robust handling of unseen words

---

## Model Architecture

```
Raw SMS Text
     │
     ▼
┌─────────────────────────────────────┐
│  BernoulliNB                        │
│  ─ alpha     : 1.0 (Laplace)        │
│  ─ binarize  : 0.0                  │
│  ─ fit_prior : True                 │
│  ─ classes   : [0 (ham), 1 (spam)]  │
└──────────────────┬──────────────────┘
                   │
                   ▼
           Prediction + Probability
```

---



## Usage

```python
import pickle

# Load the model bundle
with open("model_bundle.pkl", "rb") as f:
    model, vectorizer = pickle.load(f)

# Predict on new messages
messages = [
    "Congratulations! You've won a FREE prize. Call now to claim!",
    "Hey, are you coming to dinner tonight?"
]

X = vectorizer.transform(messages)
predictions = model.predict(X)
probabilities = model.predict_proba(X)

for msg, pred, prob in zip(messages, predictions, probabilities):
    label = "SPAM" if pred == 1 else "HAM"
    print(f"[{label}] ({prob[1]:.1%} spam confidence) → {msg}")
```

**Output:**
```
[SPAM] (96.3% spam confidence) → Congratulations! You've won a FREE prize. Call now to claim!
[HAM]  (0.0% spam confidence) → Hey, are you coming to dinner tonight?
```

---

## Model Details

| Property | Value |
|---|---|
| Algorithm | Bernoulli Naive Bayes |
| Vocabulary Size | 6,715 tokens |
| Classes | `0` = ham, `1` = spam |
| Class Prior (ham) | 0.8755 |
| Class Prior (spam) | 0.1245 |
| Laplace Smoothing (α) | 1.0 |
| Binarize Threshold | 0.0 |
| scikit-learn Version | 1.8.0 |
| Bundle Size | ~287 KB |

### Top Discriminating Features

**Spam indicators:** `free`, `call`, `txt`, `mobile`, `claim`, `reply`, `stop`, `prize`, `urgent`

**Ham indicators:** `go`, `come`, `got`, `know`, `like`, `ok`, `time`, `good`, `love`

---
