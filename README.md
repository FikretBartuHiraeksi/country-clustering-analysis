# Country Clustering & Analysis
Segmenting 185 countries into four groups by overall quality of life, using 2023-country-level data and hierarchical (Ward) clustering in Python.

# Overview
Most country comparisons rank nations by how they dominate in several areas, such as military dominance, economic size, or technological capacity. This project groups
countries by how people live instead: health, education, fertility and income per person. The aim was to practise the full data analytics workflow: cleaning, exploration, clustering and interpration.

The full write-up with all charts is in [📄 Full Project Report (PDF)](./Country%20Clustering.pdf). The code is in [📓 Jupyter Notebook](./Country%20Clustering.ipynb).

# Data
- **Dataset:** Global Country Information Dataset 2023 (`world-data-2023.csv`), 195 countries x 35 features
- **Source:** [Kaggle - Global Country Information Dataset 2023](https://www.kaggle.com/datasets/nelgiriyewithana/countries-of-the-world-2023)
- **Author:** Nidula Elgiriyage
- **License:** CC BY 4.0. The CSV in this repository is the original file, unmodified. All cleaning is done in the notebook.

# Method
1. **Diagnosis:** checked data types, nulls and distributions (histograms, box plots, correlation heatmap).
2. **Cleaning:** removed % and $ symbols and fixed data types. Dropped countries with more than 10 missing values and the minimum wage column. Imputed the remaining nulls with the column median because of outliers. Dropped Birth Rate, Infant Mortality and Maternal Mortality Ratio because they are strongly correlated with Fertility Rate and Life Expectancy. Created GDP per capita (GDP / Population) and log-transformed it.
3. **Feature selection:** Gross Tertiary Education Enrollment, Fertility Rate, Life Expectancy, GDP per capita, Physicians per thousand.
4. **Scaling:** StandardScaler. GDP per capita was additionally up-weighted by 2.5 as a manual choice, since it is the only economic feature.
5. **Clustering:** hierarchical clustering with Ward linkage, using a dendrogram and silhouette scores to choose k.
6. **Interpretation:** cluster profiles, a choropleth map, and comparisons against CO2 emissions, urbanisation, tax and armed forces size.

# Results
| Segment | Fertility rate | Life expectancy | Physicians / 1000 | Tertiary enrollment |
| :--- | :--- | :--- | :--- | :--- |
| **High Life Quality** | 1.59 | 81.6 | 3.3 | 67% |
| **Upper-Middle Life Quality** | 1.86 | 75.9 | 2.8 | 56% |
| **Developing Country** | 2.86 | 70.5 | 0.8 | 22% |
| **Poor Life Quality** | 4.68 | 61.6 | 0.2 | 8% |

# Limitations
- The silhouette score was highest at k = 2 (0.48) and fell at k = 4 (0.35). k = 4 was chosen for interpretability, so the four segments are descriptive rather than statistically optimal.
- Segment names (for example "Developing Country") are my own labels. The dataset has few direct quality-of-life measures.
- Cleaning and median imputation affect small countries most.

# Tools
- 🐍 Python 3
- 📓 Jupyter Notebook
- 🐼 pandas
- 🔢 numpy
- 🤖 scikit-learn
- 📊 seaborn
- 📈 plotly
- 🔬 scipy

## How to run
```bash
pip install pandas numpy scikit-learn seaborn plotly scipy jupyter
jupyter notebook Cluster.ipynb
```

# Author
Fikret Bartu Hıraekşi
