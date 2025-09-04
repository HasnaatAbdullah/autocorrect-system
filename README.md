# autocorrect-system
Implementation of an Autocorrect System from scratch using edit distance algorithms and Bayesian probability to predict and correct misspelled words.
# 🔠 Autocorrect System Using Edit Distance & Probability

This repository contains my implementation of an **Autocorrect System** from scratch using **Python**.  
It suggests the most likely correct words for misspelled inputs by leveraging **edit distance algorithms** and **Bayesian probability**.

---

## 🚀 Project Overview

This project demonstrates the working of an autocorrect system inspired by **Peter Norvig's algorithm**.  
It corrects spelling errors by:

1. Calculating all possible candidate words within **1 or 2 edit distances**.
2. Using a **probability-based model** to rank candidates.
3. Selecting the most likely correct word.

---

## 🧠 Concepts Implemented

- **Edit Distance**:
  - **Delete** → Remove a letter → `"hat"` → `"at"`, `"ha"`, `"ht"`
  - **Switch** → Swap two adjacent letters → `"eta"` → `"eat"`, `"tea"`
  - **Replace** → Change a letter → `"jat"` → `"hat"`, `"rat"`, `"cat"`
  - **Insert** → Add a letter → `"te"` → `"the"`, `"ten"`, `"ate"`
- **Language Modeling**:
  - Uses **word frequency counts** from a text corpus.
- **Bayesian Inference**:
  - Ranks candidates based on probability.

---

## 📌 Implementation Details

### **1. Generate Candidate Words**
All possible candidate words are generated using 1 and 2 edit distances:

```python
def delete_letter(word):
    return [word[:i] + word[i+1:] for i in range(len(word))]

def switch_letter(word):
    return [word[:i] + word[i+1] + word[i] + word[i+2:] for i in range(len(word)-1)]

def replace_letter(word):
    alphabet = 'abcdefghijklmnopqrstuvwxyz'
    return [word[:i] + c + word[i+1:] for i in range(len(word)) for c in alphabet]

def insert_letter(word):
    alphabet = 'abcdefghijklmnopqrstuvwxyz'
    return [word[:i] + c + word[i:] for i in range(len(word)+1) for c in alphabet]
