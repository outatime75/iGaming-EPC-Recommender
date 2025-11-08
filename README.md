## 🌟 README: Contextual Ranking Engine for iGaming Affiliates

This repository contains a practical, end-to-end Machine Learning demo designed to solve a core revenue optimization problem in affiliate marketing: **Contextually Ranking Brands to Maximize Expected EPC (Earnings Per Click).**

The accompanying Jupyter Notebook (`recommender_system_demo.ipynb`) is specifically tailored for the **iGaming/Affiliate** industry, blending collaborative filtering with real-time conversion propensity models and commercial payout terms. This demo serves as a powerful showcase for delivering immediate, tangible value in specialized AI workshops.

### 🎯 Overview: Maximizing Expected EPC

The system moves beyond simple historical averages to answer the key business question: *"For a given affiliate, GEO, and device, which brand will generate the highest expected revenue per click **right now**?"*

The final ranking is a **blended score** that combines two critical signals with the brand's payout structure (CPA, RevShare, Hybrid):

1.  **Long-Term Affinity (SVD Recommender):** Built on historical performance (FTDs + NGR) to understand which brands an affiliate is *most likely to succeed with*.
2.  **Short-Term Profitability (Random Forest Propensity):** Predicts the $\text{P(FTD)}$ for a specific lead, adjusted by the brand's actual CPA/RevShare terms.

### ✨ Key Features of the Demo

* **SVD Collaborative Filtering:** Utilizes `TruncatedSVD` on historical performance (FTDs + NGR) to create **Affiliate-Brand Affinity Scores**, filling in missing data points.
* **FTD Propensity Classifier:** A supervised `RandomForestClassifier` trained to predict the $\text{P(FTD)}$ based on dynamic context (GEO, Device, Hour) and static features (Affiliate Quality, Brand Baseline CR).
* **Economic Blending:** Model scores are combined with the brand's commercial terms (CPA/RevShare/Hybrid) to calculate the **Expected EPC**, ensuring recommendations are ranked by **monetary value**.
* **Offline Evaluation:** Includes a **Hit@K** validation step to prove the long-term predictive power of the SVD model against future successful affiliate-brand pairings.

---

### 💻 Technical Stack & Requirements

The demo is contained within a single executable Jupyter Notebook.

| Component | Library/Technique | Purpose |
| :--- | :--- | :--- |
| **Data Manipulation** | Pandas, NumPy | Data loading, preparation, and feature engineering. |
| **Affinity Model** | `TruncatedSVD` (Scikit-learn) | Matrix factorization for Collaborative Filtering. |
| **Propensity Model** | `RandomForestClassifier` (Scikit-learn) | Supervised classification of FTD probability. |

You will need the following Python packages (installable via `pip`):
```bash
pip install pandas numpy scikit-learn scipy matplotlib jupyter
