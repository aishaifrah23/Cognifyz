#  Restaurant Data Analysis 

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=for-the-badge&logo=Matplotlib&logoColor=black)
![Seaborn](https://img.shields.io/badge/Seaborn-4c72b0?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)

> Exploratory and advanced data analysis on 9,551 global restaurants using the Zomato dataset — completed as part of the Cognifyz Data Science Internship.

---

##  Project Structure

| File | Description |
|------|-------------|
| `level1.ipynb` | Foundational EDA — cuisine types, city density, price distribution, delivery vs rating |
| `level3.ipynb` | Advanced analysis — NLP text preprocessing, votes correlation, price vs service breakdown |
| `Dataset .csv` | Zomato dataset — 9,551 rows, 21 columns |
| `task1_text_analysis.py` | Standalone script for Task 1 (text analysis) |
| `task2_votes_analysis.py` | Standalone script for Task 2 (votes analysis) |
| `task3_price_services.py` | Standalone script for Task 3 (price vs services) |

---

##  Level 1  Exploratory Data Analysis

### Task 1 · Cuisine Type Analysis
- Inspected dtype and missing values in the `Cuisines` column
- Filled missing values with `'Unknown'`, then split multi-cuisine rows using `.str.split(', ').explode()`
- Extracted top 3 cuisines by frequency using `.value_counts()`
- Calculated percentage share of each top cuisine out of total exploded records

### Task 2 · City-Level Restaurant Density
- Used `.value_counts()` on `City` to find the most restaurant-dense city
- Computed mean rating per city with `groupby('City')['Aggregate rating'].mean()`
- Sorted descending and identified the top 5 highest-rated cities

### Task 3 · Price Range Distribution
- Confirmed 4 distinct pricing tiers (1 = Budget → 4 = Premium)
- Calculated absolute count and % share per tier
- Visualised with `sns.countplot()` using viridis palette and saved as `price_range_distribution.png`

### Task 4 · Online Delivery vs Rating
- Calculated % of restaurants offering online delivery
- Segmented into delivery vs no-delivery groups
- Compared average ratings across both groups with a printed conclusion

---

##  Level 3  Advanced Analysis

### Task 1 · Text Analysis (NLP)
- Preprocessed `Cuisines` column: `fillna('')`, lowercase, regex to strip special characters
- Frequency-based keyword extraction using `collections.Counter` with stop word filtering
- Separated into high-rated (≥ 4.5) and low-rated (≤ 2.5) groups
- Applied **VADER Sentiment Analysis** on `Rating text` column to assign polarity scores; grouped words where `polarity > 0.5` (positive) and `< -0.5` (negative)
- Plotted average cuisine text length per rating tier using scatter + line chart

### Task 2 · Votes Analysis
- Found extremes: **Toit** holds max votes (10,934), 1,094 restaurants have 0 votes
- Pearson correlation between votes and rating: **r = 0.31** (weak-to-moderate positive)
- Visualised with `sns.regplot()` with 95% confidence interval band

### Task 3 · Price Range vs Services
- Converted Yes/No columns to binary with `.map({'Yes': 1, 'No': 0})`
- Computed service availability % per tier using `groupby().mean() * 100`
- Created grouped and stacked bar charts saved as `task3_price_vs_services.png`

| Price Tier | Online Delivery | Table Booking |
|------------|----------------|---------------|
| Tier 1 (Budget) | 15.8% | 0.02% |
| Tier 2 | 41.3% | 7.7% |
| Tier 3 | 29.2% | 45.7% |
| Tier 4 (Premium) | 9.0% | 46.8% |

>  Online delivery peaks at Tier 2 then drops. Table booking rises sharply at Tiers 3–4 — premium restaurants prioritise in-dining over delivery.

---

##  Setup

```bash
# install via mamba (conda environment)
mamba install pandas matplotlib seaborn

# vaderSentiment requires pip
pip install vaderSentiment

# launch notebooks
jupyter notebook level1.ipynb
jupyter notebook level3.ipynb
```

---

##  Key Findings

- **North Indian** cuisine dominates across all rating levels — it's the largest category, spanning both extremes
- **More votes ≠ guaranteed quality** — r = 0.31 shows a real but loose relationship
- **Budget restaurants** barely offer table booking (0.02%) while premium ones embrace it (~47%)
- **Delivery is a mid-tier thing** — Tier 2 restaurants offer it most, budget and premium restaurants both avoid it

---

*Cognifyz Data Science Internship · Zomato Dataset · 9,551 restaurants*
