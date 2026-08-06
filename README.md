# Anime Recommendation System

A content-based anime recommendation engine that matches user preferences to anime titles using **TF-IDF Vectorization** and **Cosine Similarity** 
---

## Table of Contents

- [Overview](#overview)
- [How It Works](#how-it-works)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Algorithm Details](#algorithm-details)
- [Demo Examples](#demo-examples)
- [Cold Start Handling](#cold-start-handling)
- [Future Improvements](#future-improvements)

---

## Overview

This project implements a **Content-Based Filtering** recommendation system. Unlike collaborative filtering (which needs lots of user interaction data), content-based filtering works immediately by matching item attributes (genres, themes) to user preferences.

**Key Features:**
- Takes user input (genre preferences)
- Matches preferences using TF-IDF + Cosine Similarity
- Displays ranked anime recommendations
- Handles cold start with trending fallback
- Interactive CLI with session history

---

## How It Works

The system follows the **Input-Process-Output (IPO)** model:

```
┌─────────────┐     ┌─────────────────────┐     ┌──────────────┐
│   INPUT     │────▶│      PROCESS        │────▶│   OUTPUT     │
│ (User State)│     │  (Similarity Logic) │     │ (Top-N List) │
└─────────────┘     └─────────────────────┘     └──────────────┘
```

### The 4-Step Pipeline

| Step | Name | Description |
|------|------|-------------|
| 1 | **Ingestion** | Capture user's genre preferences (minimum 3 recommended) |
| 2 | **Scoring** | Calculate cosine similarity between user vector and all anime vectors |
| 3 | **Sorting** | Order results by similarity score (highest first) |
| 4 | **Filtering** | Return Top-N recommendations to prevent information overload |

---

## Project Structure

```
anime_recommender/
├── data/
│   └── anime_data.csv          # Dataset with 100 anime titles
├── src/
│   ├── recommender.py          # Core recommendation engine
│   └── cli.py                  # Interactive CLI application
├── notebooks/
│   └── analysis.ipynb          # (Optional) Data analysis notebook
├── screenshots/
│   └── demo.png                # Screenshot of system in action
├── requirements.txt            # Python dependencies
├── .gitignore                  # Git ignore rules
└── README.md                   # This file
```

---

## Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/anime-recommender.git
cd anime-recommender

# Create virtual environment (recommended)
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

---

## Usage

### Quick Start (Demo Mode)

Run the recommender with built-in demo examples:

```bash
python src/recommender.py
```

This will run three demo scenarios and then prompt for your own preferences.

### Interactive CLI Mode

For the full interactive experience:

```bash
python src/cli.py
```

The CLI provides:
- Get personalized recommendations
- Browse available genres
- View session history
- Save recommendations to JSON
- ℹLearn about the algorithm

---

## Algorithm Details

### TF-IDF Vectorization

**Why not just count overlapping tags?**

Simple binary vectors (1 = present, 0 = absent) treat generic words the same as specific ones. TF-IDF solves this by:

- **Term Frequency (TF)**: Terms appearing more frequently in an item are more representative
- **Inverse Document Frequency (IDF)**: Penalizes terms that appear across too many items (like generic genres)

**Formula:**
```
TF-IDF(t, d) = TF(t, d) × IDF(t)

where:
TF(t, d) = count of term t in document d / total terms in d
IDF(t)   = log(Total Documents / Documents with term t)
```

The logarithm acts as a **dampening effect**, keeping values comparable.

### Cosine Similarity

**Why not Euclidean distance?**

Euclidean distance is sensitive to vector magnitude. If two anime share identical tags but one has a larger feature set, Euclidean distance gives a high (bad) score.

Cosine similarity measures the **angle between vectors**, making it **invariant to magnitude**:

```
cos(θ) = (A · B) / (||A|| × ||B||)
```

**Score Interpretation:**
- **1.0** → Perfectly aligned (identical orientation)
- **0.0** → Orthogonal (no common characteristics)
- Range for TF-IDF: **0 to 1** (since values are non-negative)

---

## Demo Examples

### Example 1: Action & Adventure Fan
```
Preferences: ["Action", "Adventure", "Fantasy"]

Top Recommendations:
#1 Attack on Titan        - 95.2% match
#2 Fullmetal Alchemist    - 91.8% match
#3 Demon Slayer           - 89.4% match
```

### Example 2: Romance & Drama Lover
```
Preferences: ["Romance", "Drama", "Slice of Life"]

Top Recommendations:
#1 Your Lie in April       - 93.7% match
#2 Clannad                - 90.1% match
#3 Violet Evergarden      - 87.5% match
```

### Example 3: Sci-Fi & Mecha Fan
```
Preferences: ["Sci-Fi", "Mecha", "Psychological"]

Top Recommendations:
#1 Code Geass              - 94.3% match
#2 Neon Genesis Evangelion - 92.1% match
#3 Psycho-Pass            - 88.9% match
```

---

## Cold Start Handling

The **Cold Start Problem** occurs when a new user has no history (profile vector = all zeros).

**Solutions implemented:**
1. **Onboarding**: Force ingestion step — require minimum 3 preferences
2. **Trending Fallback**: Default to "Very High" popularity anime if no valid preferences
3. **Genre Validation**: Only accept genres that exist in the vocabulary

---

## Future Improvements

- [ ] Add synopsis-based keyword extraction using NLP (NLTK/spaCy)
- [ ] Implement user rating system for collaborative filtering hybrid
- [ ] Add anime poster images and trailers
- [ ] Deploy as a web app using Flask/Streamlit
- [ ] Integrate with MyAnimeList API for real-time data
- [ ] Add recommendation explanation (why this anime was recommended)
- [ ] Implement diversity filtering (avoid too similar recommendations)

---
