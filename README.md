# Cocktail Network Analysis

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg)](https://www.python.org/)

A **network science** approach to analyzing cocktail recipes. This Jupyter notebook explores ingredient relationships, recipe complexity, and builds recommendation tools using graph theory.

---

## Overview

This project transforms raw cocktail data into powerful network insights:

- **Bipartite Graph**: Connects drinks to their ingredients.
- **Co-occurrence Network**: Shows which ingredients appear together most often.
- **Community Detection**: Finds clusters of ingredients that define cocktail "families".
- **Centrality Analysis**: Identifies the most influential ingredients.
- **Complexity Scoring**: Ranks drinks by difficulty (Beginner to Advanced).
- **Smart Recommendations**:
  - What can I make with my pantry?
  - What’s *almost* makeable (missing just 1 ingredient)?
  - Best substitutes for missing ingredients.

---

## Features

| Feature | Description |
|-------|-----------|
| **Graph Construction** | Bipartite + weighted co-occurrence using `networkx` |
| **Community Detection** | Louvain algorithm (or fallback greedy modularity) |
| **Centrality Measures** | Degree, Betweenness, Closeness, Eigenvector (projected) |
| **Recipe Complexity** | Score = 0.5×#ingredients + 0.5×#categories |
| **Makeable Drinks** | Exact match with available ingredients |
| **Near-Makeable** | Ranked by Jaccard similarity (top 3, max 1 missing) |
| **Substitutes** | Same-category + co-occurrence weighted |
| **Visualization** | Top 15 ingredients by 3 centralities (1×3 bar plot) |

---

## Data

Place these files in a `data/` folder:

```text
data/
├── drinks.csv      ← Raw recipes (drink name + strIngredient1..15)
└── cleaning.csv    ← Id (raw), standardized_name, category
```

> Example `cleaning.csv`:
> ```csv
> Id,standardized_name,category
> "light rum","light rum","rum"
> "bourbon","bourbon","whiskey"
> ```

---

## Requirements

```bash
pip install pandas numpy networkx matplotlib seaborn python-louvain
```

---

## Usage

```bash
# 1. Clone the repo
git clone https://github.com/your-username/cocktail-network-analysis.git
cd cocktail-network-analysis

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch Jupyter
jupyter notebook
```

Open `network_science_final.ipynb` and run all cells.

---

## Key Functions

```python
find_makeable_drinks(["vodka", "lime juice", "ginger beer"]) 
# → ['Moscow Mule']

find_near_makeable_drinks(available, max_missing=1, top_n=3)
# → Drinks missing ≤1 ingredient, ranked by similarity

find_substitutes("triple sec", n_suggestions=5)
# → ['cointreau', 'grand marnier', ...]
```

---

## Project Structure

```text
cocktail-network-analysis/
├── network_science_final.ipynb   ← Main analysis notebook
├── data/
│   ├── drinks.csv                ← Raw cocktail data
│   └── cleaning.csv              ← Ingredient mapping
├── README.md                     ← This file
```