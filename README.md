# Market Basket Analysis using Association Rules on Online Retail Data

This project implements **Market Basket Analysis** using the **Apriori Algorithm** and **Association Rules Mining** on retail transaction data. The goal is to discover strong relationships, buying patterns, and cross-selling opportunities among products frequently purchased together.

---

## Project Overview
Using transactional data containing lists of customer purchases, this notebook performs comprehensive data preprocessing, transforms row-level text data into binary format via one-hot encoding, extracts frequent itemsets, and generates actionable association metrics such as **Support**, **Confidence**, and **Lift**.

---

## Tech Stack & Library Dependencies
The project is built entirely in Python inside a Jupyter Notebook environment. The required packages include:

*   **Pandas**: For robust data manipulation and cleaning.
*   **Openpyxl**: Engine used to read Excel (`.xlsx`) spreadsheets.
*   **Mlxtend (Machine Learning Extensions)**: For deploying the `apriori` and `association_rules` mining pipelines.

---

## Data Pipeline & Implementation
## 1. Data Cleaning & Preprocessing
*   **File Loading**: Loads transaction details from Online_retail.xlsx.

*   **Shape & Information**: Investigates basic profiles (.info(), .dtypes) and ensures zero missing values exist across records.

*   **Deduplication**: Drops duplicated transaction histories, reducing the initial dataset down to 5,175 unique market baskets to remove redundancy and bias.
  
---

## 2. Market Basket Formatting (One-Hot Encoding)
Because transactions are loaded as comma-separated string records within a single column, we unpack and map them cleanly:

Utilizes .str.get_dummies(',') to convert string data into a structured binary DataFrame matrix.

The output produces a sparse dataframe with 120 unique product features (columns) tracking the presence (1) or absence (0) of a product per basket.

---

## 3. Frequent Itemset Generation (Apriori)
The Apriori algorithm is configured using hyperparameter tuning across two support thresholds to extract meaningful patterns:

*   **High Constraint Exploration:** Evaluated with a min_support=0.05 to capture strictly dominant single items and high-volume pairs (e.g., Mineral Water, Spaghetti, Chocolate).

*   **Granular Deep Dive:** Loosened to min_support=0.02 to discover hidden, multi-item relationships (3-item rules like {milk, spaghetti} -> {mineral water}).

---

## 4. Association Rules Generation & Insights
Rules are filtered and sorted using fundamental data science metrics:

*   **Highest Lift:** Identifies highly dependent combinations. The top rule discovered is {herb & pepper} <-> {ground beef} with a Lift of ~2.53, proving strong statistical synergy.

*   **Highest Confidence:** Explores structural likelihoods. Buying {soup} or combos like {milk, spaghetti} yields a ~45% to 47% probability of the customer adding {mineral water} to their cart.

---

## Key Analytical Definitions & Formula Concepts
*   **Support:** The popularity of an itemset. The ratio of transactions containing the itemset divided by the total number of records.
*   **Confidence:** The directional reliability of the rule. Given itemset $A$ is purchased, it represents the conditional probability that itemset $B$ will also appear ($P(B|A)$).
*   **Lift:** Measures how much more often $A$ and $B$ occur together than expected if they were statistically independent. A value $> 1$ indicates that the items positively reinforce each other's sales.

---

## Challenges & Limitations of Association Mining
While highly effective for strategic merchandising, this notebook highlights the core trade-offs of Association Rule Mining:
*   **Threshold Sensitivity:** Setting support thresholds too high yields empty insights, while setting them too low floods results with bloated or "boring" rules.

*   **Rule Explosion:** Large or highly diverse transactional datasets generate massive amounts of uninteresting patterns, demanding careful programmatic sorting via Lift and Leverage.

To install these dependencies locally, run:
```bash
pip install pandas openpyxl mlxtend
