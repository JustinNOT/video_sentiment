# 🎬 Moving Sentiment Analysis on Video Clips

## 📌 Overview

This project explores **multi-modal sentiment analysis** on YouTube movie clips. We aim to understand and track **emotions as they evolve over time** in a video, using information from user comments, audio soundtrack, and transcript dialogues.

The project is split into two major parts:
- **Model A**: Predicts the overall emotion of a video clip based on YouTube comments.
- **Model B**: Dynamically tracks changing emotions in a video using transcript, soundtrack, and image-based models.

---

## 🧠 Models

### 🧾 Model A: YouTube Comment-Based Emotion Classifier

This model predicts a video clip’s overall emotion using the top 50 English-language comments on the clip.

- **Model**: XGBoost Classifier
- **Input**: Top 50 most-liked comments per clip
- **Output**: One of four emotions — `Neutral`, `Funny`, `Fear`, `Sad`
- **Dataset**:
  - 7,000 hand-labeled YouTube comments
  - Non-English and irrelevant comments filtered out
- **Performance**:  
  - **Accuracy**: 86% on a 4-class classification task

---

### 🎥 Model B: Dynamic Clip Sentiment Analysis

A multi-stream model that tracks sentiment **over time** in a video clip using three modalities:

#### 1️⃣ Transcript Model
- **Goal**: Predict emotion per line of dialogue
- **Model**: Text classifier (architecture unspecified)
- **Dataset**: 
  - Primary: [DailyDialog](https://aclanthology.org/I17-1099/)
  - Exploring: [CMU-MOSEI](https://github.com/A2Zadeh/CMU-MultimodalSDK)
- **Status**: 
  - 86% accuracy on current dataset
  - Progress stalled due to class imbalance
- **Input**: Sentence-level dialogue
- **Output**: One of six emotion labels per sentence

#### 2️⃣ Soundtrack Model
- **Goal**: Predict **valence/arousal (V/A)** values every 0.5s across 30s clip segments
- **Model**: Regression model (architecture unspecified)
- **Dataset**: [DEAM / EmoMusic Dataset](https://github.com/metalbubble/DEAM)
- **Input**: 15s–45s audio snippet
- **Output**: V/A pair every 0.5s
- **Performance**: 
  - **MSE**: 0.0280
  - Status: Fully trained and functioning well

#### 3️⃣ Image Model (Development Paused)
- **Components**:
  - **Bounding Box Detector**
    - Dataset: LFPW
    - Output: 4 facial bounding box coordinates
    - Status: High accuracy
  - **Facial Emotion Recognition**
    - Datasets used: WIDERFace, FDDB
    - Issues:
      - Emotion labels do not align with intended use
      - Labels are ambiguous and context-insensitive
      - No suitable replacement dataset available
    - Status: Development paused; focus shifted to audio and text

---

## 🧪 Dataset Summary

| Modality   | Dataset(s) Used                     | Notes |
|------------|-------------------------------------|-------|
| Comments   | Manually collected YouTube comments | 7,000 labeled, top-liked only, English-only |
| Transcript | DailyDialog, CMU-MOSEI              | Sentence-level emotion labels |
| Audio      | DEAM / EmoMusic                     | V/A labels every 0.5s |
| Image      | LFPW, WIDERFace, FDDB               | Face detection working; emotion labels unsuitable |

---