# Web-Based E-Commerce Product Recommendation System Using Association Rule Mining

Market-basket analysis of 7,501 grocery transactions, extended into a working
product recommendation system. Apriori and FP-Growth find frequently bought
product combinations, association rules are generated, and the rules are used
to recommend products based on the items a user selects.

**Notebooks**
- `recommendation_system.ipynb`: recommendation engine, evaluation and user interface (main project)
- `association_rule_mining.ipynb`: detailed mining and statistical analysis (supporting work)

## Problem statement
Online shopping platforms contain large numbers of product purchase
transactions. Identifying relationships between products can help recommend
relevant products to customers based on the items they are currently
interested in. This project builds an association-rule-based recommendation
system: frequently co-purchased products are mined, and rules are used to
suggest additional products for a selected basket.

## Objectives
1. Clean the data and build transactions.
2. Mine frequent itemsets with Apriori and FP-Growth.
3. Generate association rules (support, confidence, lift).
4. Build a recommender that suggests up to 5 products for a selected basket.
5. Evaluate it with an 80/20 holdout split (Precision@5, Recall@5, Hit Rate@5, Coverage).
6. Provide a simple interactive interface.

## Dataset
- File: `data/original_dataset.csv` (original name: `store_data_association_rules.csv`)
- Source: [add publisher / download link here]
- License / usage: [add licence or "publicly available for educational use"]
- 7,501 transactions, 119 distinct products, no header row, average basket size about 3.9
- No personal or customer-identifying information (no customer IDs, names or timestamps)

## Method
1. Load data (no header), trim item names, build one basket per row.
2. Split transactions 80% train / 20% test (`random_state=42`).
3. Rules are mined on **training data only**, so there is no test leakage.
4. FP-Growth with min support 0.005, then rules with confidence >= 0.20 and lift >= 1.2.
5. Recommendation: for the selected items, find rules whose antecedent is contained in the basket, and rank the consequents by lift, then confidence (top 5).
6. Fallback: if no rule matches (rare items), the interface shows the most popular products.
7. Evaluation: for each test basket, half of the items are the input and the rest are the relevant items.
8. Interface: an interactive `ipywidgets` selector and Recommend button.

## Parameters
| Parameter | Value |
|---|---|
| Minimum support | 0.005 |
| Minimum confidence | 0.20 |
| Minimum lift | 1.2 |
| Recommendations | 5 |
| Train / test split | 80 / 20 |
| Random seed | 42 |

## Results
| Metric | Value |
|---|---|
| Precision@5 | [paste from notebook] |
| Recall@5 | [paste from notebook] |
| Hit Rate@5 | [paste from notebook] |
| Coverage | [paste from notebook] |

Example: selecting *burgers* or *ground beef* returns products with
confidence, lift and support. Apriori and FP-Growth produce identical
itemsets; FP-Growth is faster at low support.

## How to run
1. Open `recommendation_system.ipynb` in Google Colab.
2. Click **Runtime, then Run all**.
3. When asked, upload `data/original_dataset.csv`.
4. Select products in the Basket box (Ctrl+click for several) and click **Recommend**.

Requirements: pandas, mlxtend, scikit-learn, ipywidgets (installed in Colab).

## Limitations
- No customer IDs, timestamps or prices; baskets are treated as sets.
- Items with low support have no rules at the chosen threshold, so a popularity fallback is used.
- Rules show association, not causation.
- Evaluation is offline on one dataset.

## Ethics
The dataset contains no personally identifiable information.
