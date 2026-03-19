<h1 align="center">WSD Project</h1>
<p align="center">
  <b>Word Sense Disambiguation through contextual embeddings, centroid-based classification, and geometric error analysis</b>
</p>

<p align="center">
  <img alt="Python" src="https://img.shields.io/badge/Python-3.10%2B-blue">
  <img alt="Jupyter" src="https://img.shields.io/badge/Jupyter-Notebook-orange">
  <img alt="Transformers" src="https://img.shields.io/badge/HuggingFace-Transformers-yellow">
  <img alt="NLTK" src="https://img.shields.io/badge/NLTK-SemCor-green">
  <img alt="Status" src="https://img.shields.io/badge/status-academic%20project-success">
</p>

---

## Overview

This project explores **Word Sense Disambiguation (WSD)** using contextual embeddings from **DeBERTa-v3-base** and a simple but interpretable **nearest-centroid classifier**.

The work was inspired by the paper:

> **How Much Do Encoder Models Know About Word Senses?**

The main goal is not only to apply a WSD pipeline, but also to analyze **when and why a simple centroid-based decision rule fails**, even when the embedding space already contains meaningful semantic structure.

---

## Motivation

A single word can express different meanings depending on context.

For example:

- **bank** → financial institution  
- **bank** → river bank

Modern encoder models produce contextual word embeddings, so the natural question is:

> **Do these embeddings already encode word meaning well enough, even before task-specific fine-tuning?**

This project studies that question on real data and then goes one step further: it examines the **limitations of centroid-based classification** in the embedding space.

---

## Project goals

- extract contextual embeddings for target words from **SemCor**
- build sense-specific centroids for each lemma
- classify test examples using **cosine similarity**
- visualize embeddings in 2D using **PCA** and **t-SNE**
- identify systematic errors of the nearest-centroid method
- compare geometric intuition from visualizations with the actual decision rule in the original high-dimensional space

---

## Method

### 1. Contextual embeddings
For each target occurrence, the model produces a contextual representation of the word in its sentence.

If a word is split into several subword tokens, their embeddings are averaged.

### 2. Sense centroids
For each sense of a lemma, embeddings of training examples are collected and averaged into a **centroid**.

### 3. Classification
For a test occurrence, its embedding is compared with all centroids of the same lemma and part of speech.

The predicted sense is the one with the **maximum cosine similarity**.

### 4. Visualization
To study the geometry of the embedding space, the project uses:

- **PCA** — better for global structure
- **t-SNE** — better for local neighborhoods

These methods are used **only for visualization**, not for classification itself.

---

## Main idea

If the encoder truly separates meanings, then occurrences of the same sense should form a coherent region in embedding space.

The centroid method assumes that:

- each sense can be represented by a single mean vector
- cosine similarity to this mean is enough to determine the correct sense

This project tests where that assumption works — and where it breaks.

---

## Repository structure

```text
wsd_project/
├── figures/
│   ├── table_pca.png
│   ├── table_pca_errors.png
│   ├── table_tsne.png
│   ├── table_tsne_errors.png
│   ├── yard_pca.png
│   ├── yard_pca_errors.png
│   ├── yard_tsne.png
│   └── yard_tsne_errors.png
├── wsd_final.ipynb
└── .gitignore
