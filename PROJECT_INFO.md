# Project Info

**Project Name:** Anime Recommendation System
**Training Program:** DecodeLabs AI Industrial Training
**Batch:** 2026
**Project Number:** 3
**Topic:** AI Recommendation Logic

## Learning Objectives
- Understand Content-Based Filtering vs Collaborative Filtering
- Implement TF-IDF Vectorization for feature weighting
- Apply Cosine Similarity for preference matching
- Build a complete Input-Process-Output recommendation pipeline
- Handle the Cold Start problem

## Technologies Used
- Python 3.8+
- Pandas (data handling)
- NumPy (numerical operations)
- Standard Library (math, collections, json)

## Submission Checklist
- [x] Dataset created (anime_data.csv)
- [x] Core engine implemented (recommender.py)
- [x] CLI interface built (cli.py)
- [x] README documentation complete
- [x] Unit tests written
- [x] Jupyter notebook for analysis
- [x] Requirements file
- [x] Git repository initialized

## Notes for Reviewer
This project strictly follows the DecodeLabs Project 3 methodology:
- Content-Based Filtering (not Collaborative)
- TF-IDF for feature weighting
- Cosine Similarity for scoring
- 4-Step Pipeline: Ingestion → Scoring → Sorting → Filtering
- Cold Start handling with trending fallback
