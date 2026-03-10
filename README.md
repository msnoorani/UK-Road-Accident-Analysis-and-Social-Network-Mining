# UK Road Accidents and Social Network Analysis

> **University of Hull**  
> Author: Muhammad Salahuddin

---

## 📌 Project Overview

This project applies **big data and data mining techniques** to two real-world datasets:

- **Part A:** UK road accident data (2019) from a government SQLite database — spatiotemporal analysis, association rule mining, clustering, and time series forecasting to advise the Department for Transport (DfT) on policy interventions
- **Part B:** Facebook social network data (SNAP) — graph construction, edge betweenness centrality, and community detection

---

## 🗂️ Datasets

| Dataset | Source | Description |
|---------|--------|-------------|
| `accident_data_v1.0.0_2023.db` | UK Dept for Transport (STATS19) | SQLite database — accident, vehicle, casualty tables for 2019 |
| `facebook_combined.txt` | Stanford SNAP | Facebook ego-network edge list — 4,039 nodes, 88,234 edges |

---

## 📊 Part A — Road Accident Analysis

### Techniques Applied
- **Spatiotemporal Analysis** — hourly and daily accident distributions
- **Association Rule Mining** — Apriori algorithm on accident severity
- **Geospatial Clustering** — KMeans with Folium interactive maps
- **Time Series Forecasting** — weekly accident prediction across 3 police forces
- **LSOA-level forecasting** — daily accident prediction for Hull's top 30 high-incident areas

---

### Key Findings

**1. When do accidents peak?**
- Most accidents occur at **18:00 on Fridays** — consistent with evening rush-hour commuter traffic
- Peak day: **Friday (Day 6)**; peak hour: **18:00**

**2. Motorcycle accidents**
| Category | Peak Hour | Peak Day |
|----------|-----------|----------|
| 125cc and under | 17:00 | Friday |
| 125cc–500cc | 17:00 | Friday |
| Over 500cc | 17:00 | Sunday |

> Over 500cc bikes peak on **Sundays** — reflecting leisure riding patterns rather than commuting

**3. Pedestrian accidents**
- Peak time: **15:30 on Fridays** — school run and early afternoon traffic
- Most occurred on dry roads under daylight conditions

**4. Apriori Association Rules**
- Variables selected via correlation heatmap: speed limit, junction detail, urban/rural area, sex of driver, first point of impact
- Min support: 0.02 | Min confidence: 0.2
- Rules revealed strong associations between **higher speed limits + rural areas → fatal/serious severity**

**5. Regional Clustering — Kingston upon Hull, East Riding of Yorkshire**
- **KMeans (k=5)** applied to latitude/longitude coordinates
- Elbow method used to determine optimal k
- Interactive **Folium maps** generated for each region
- Hull clusters revealed accident hotspots concentrated around A-road junctions and city centre areas

**6. Time Series Forecasting (3 Police Forces)**
- Historical data: 2017–2018 weekly counts
- Forecast target: 2019 weekly counts
- Models compared against actual 2019 data per police force

**7. LSOA Hull — Daily Forecasting**
- Top 30 LSOAs by accident count (Jan–Mar 2019) identified
- Aggregated time series built for Jan–Jun 2019
- Model used to forecast **daily accident occurrences for July 2019**

---

### Data Cleaning
- Connected to SQLite database using `sqlite3` — extracted accident, vehicle, casualty tables for 2019
- Missing coordinates imputed using **mode by ONS district**
- Negative values (-1) per STATS20 guidelines replaced with `np.nan`
- **KDE imputation** (Gaussian kernel, bandwidth=2) used for remaining numeric nulls
- Invalid codes (0, 9, 99) per STATS20 reference corrected across all three tables
- Tables merged on `accident_index` for unified analysis

---

## 🔗 Part B — Facebook Social Network Analysis

### Network Characteristics

| Property | Value |
|----------|-------|
| Nodes | 4,039 |
| Edges | 88,234 |
| Network Density | 0.010819 |
| Average Degree | 43.69 |

### Edge Betweenness Centrality
- Computed for all 88,234 edges
- Distribution is **highly right-skewed** — a small number of edges act as critical bridges between communities
- High betweenness edges likely connect different social circles

### Community Detection — Algorithm Comparison

| Algorithm | Communities Detected |
|-----------|---------------------|
| **Louvain** | 15 |
| **Label Propagation** | ~17–20 (variable) |

**Louvain top communities:**
- Largest community: ~600+ nodes
- Louvain modularity score computed — indicating strong community structure
- Mean clustering coefficient calculated per community

**Comparison:**
- Louvain produced more stable, consistent results across runs
- Label Propagation is faster but produces variable community boundaries due to random initialisation
- Both algorithms revealed clear community structure consistent with real-world social groupings (friend circles, university networks)

---

## 🛠️ Tech Stack

**Part A:**
- `sqlite3` — database connection and SQL queries
- `Pandas`, `NumPy` — data manipulation
- `Matplotlib`, `Seaborn` — visualisations
- `mlxtend` — Apriori algorithm and association rules
- `scikit-learn` — KMeans clustering, MinMaxScaler, KernelDensity imputation
- `Folium` — interactive geospatial maps
- `SMOTE / RandomUnderSampler` — class balancing

**Part B:**
- `NetworkX` — graph construction, edge betweenness centrality
- `python-louvain` — Louvain community detection
- `NetworkX label_propagation_communities` — Label Propagation
- `Matplotlib` — network visualisations

---

## 📁 Repository Structure

```
├── part_a_coding.ipynb      # Road accident analysis notebook
├── part_b_coding.ipynb      # Social network analysis notebook
├── README.md                # Project documentation
└── data/
    └── README.md            # Dataset instructions
```

---

## 📥 Datasets

See `data/README.md` for setup instructions.

- **Part A:** UK STATS19 accident database — available via UK Dept for Transport open data portal
- **Part B:** Facebook SNAP dataset — [Stanford SNAP](https://snap.stanford.edu/data/ego-Facebook.html)

---

## 🏛️ Policy Recommendations (Part A)

Based on the analysis, key recommendations to the Department for Transport:

1. **Increase enforcement on Fridays 17:00–19:00** — peak accident window nationally
2. **Target speed reduction measures on rural A-roads** — Apriori rules link high speeds + rural areas to fatal outcomes
3. **Improve pedestrian infrastructure near schools** — pedestrian peak at 15:30 aligns with school dismissal
4. **Deploy motorcycle safety campaigns for leisure riders** — over 500cc bikes peak on Sundays, not commute days

---

## 👤 Author

**Muhammad Salahuddin**  
MSc Artificial Intelligence & Data Science — University of Hull  
[GitHub](https://github.com/msnoorani) | [LinkedIn](https://linkedin.com/in/msnoorani)
