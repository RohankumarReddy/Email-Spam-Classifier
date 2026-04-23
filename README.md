<h1 align="center">📩 SMS Spam Classifier</h1>
<p align="center">
  <img src="https://i.imgur.com/uCbB9nD.gif" alt="Spam Detection Demo" width="400"/>
</p>

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.8.0-orange?logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Model: BernoulliNB](https://img.shields.io/badge/Model-BernoulliNB-purple)](https://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.BernoulliNB.html)

A lightweight, production-ready Email/SMS spam detection system built with a **Bernoulli Naive Bayes** classifier. Trained on the [Spam Email Classification Dataset](https://www.kaggle.com/datasets/phangud/spamcsv), the model distinguishes ham (legitimate) messages from spam with a vocabulary of **6,715 features**.

---


**Key characteristics:**
- Binary classification: `0 = ham`, `1 = spam`
- Class distribution: ~87.6% ham / 12.4% spam (reflects real-world SMS imbalance)
- Vocabulary: 6,715 unigram features extracted from SMS text
- Laplace smoothing (α = 1.0) for robust handling of unseen words


**Spam indicators:** `free`, `call`, `txt`, `mobile`, `claim`, `reply`, `stop`, `prize`, `urgent`

**Ham indicators:** `go`, `come`, `got`, `know`, `like`, `ok`, `time`, `good`, `love`

