# Customer Segmentation on Online Retail (K-Means, Agglomerative, DBSCAN/HDBSCAN) + Cluster-Based Recommendations

## Abstract 
This project presents a comprehensive machine-learning framework for enhancing online retail analytics through data-driven customer segmentation and targeted product recommendation. Leveraging the publicly available 2010–2011 transactional dataset from a UK-based retailer, the study implements an end-to-end pipeline spanning rigorous data cleaning, feature engineering, and unsupervised learning techniques.

After imputing anomalies and transforming raw transactions into a customer-centric matrix of normalised RFM metrics and behavioural attributes, a multi-model clustering strategy is applied. K-Means supplies an interpretable baseline; Hierarchical Agglomerative Clustering offers a nuanced multilevel perspective on customer relations; and DBSCAN/HDBSCAN detect low-density outliers to preserve segment purity.

Cluster evaluation is guided holistically by Silhouette Score, Calinski-Harabasz Index, and Davies-Bouldin Index. Optimal model selection, based on the peak silhouette value of 0.53, yields three behaviourally distinct clusters. These segments are profiled to reveal purchasing propensities and lifetime-value potential, and are subsequently integrated into a cluster-based recommendation engine that promotes top-selling yet unpurchased products within each cluster. 

The proposed framework demonstrates a replicable, end-to-end, multi-intelligence system for online retailers to refine marketing campaigns, elevate personalisation, and stimulate revenue growth through data-driven customer insights.

## Keywords
*RFM Analysis • Unsupervised Learning • K-Means Clustering • Hierarchical Agglomerative Clustering • DBSCAN • HDBSCAN • Silhouette Score • Customer Segmentation • Recommendation System • Content-Based Filtering • Online Retail Analytics*

---

## **TL;DR.** 
We cluster ~4k retail customers using a PCA-compressed feature set and compare three methods.  
*Final take:* **K-Means (k=3)** gives the clearest three actionable segments; Agglomerative corroborates the structure; HDBSCAN is best kept for anomaly surfacing.

Beyond clustering, we built a **cluster-driven recommendation logic**:
  - Top-3 product not-yet-bought suggestions tailored for each cluster profile.


## Notebooks
- **K-Means** — [`01_kmeans.ipynb`](notebooks/01_kmeans.ipynb)
- **Agglomerative** — [`02_agglomerative.ipynb`](notebooks/02_agglomerative.ipynb)
- **DBSCAN/HDBSCAN** — [`03_dbscan_hdbscan.ipynb`](notebooks/03_dbscan_hdbscan.ipynb)

## Data & Features
- 4,067 customers × 16 engineered features -> **z-scored** + outlier freed, then **PCA to 6 components**, ~**81%** variance retained. The PCA matrix feeds all three clustering methods.

## Results (on the 4,067×6 PCA matrix)
| Model                                | #Clusters (noise) | Silhouette | Calinski–Harabasz | Davies–Bouldin | Take |
|-------------------------------------|-------------------:|-----------:|------------------:|---------------:|------|
| **K-Means (k=3)**                    | 3 (0%)            | **0.236**  | **1257.17**       | 1.37           | Tight, distinct three-segment split. :contentReference[oaicite:1]{index=1} |
| **Agglomerative (complete, k=3)**    | 3 (0%)            | **0.367**  | 507.64            | 1.27           | Highest cohesion; supports k=3 decision. |
| **HDBSCAN (min_cluster_size=50)**    | 2 (+ **7.8%** noise) | 0.260   | 852.42            | **1.15**       | Great for outlier flagging; under-segments for marketing. 

PCA removes redundancy, speeds clustering, keeps structure; 6 PCs captured ~81% while remaining interpretable via loadings. 

## Reproduce
```bash
pip install -r requirements.txt
jupyter lab
# open notebooks/ and run top to bottom
```

## Final Deliverables:
  - **Clean, runnable notebooks** for three clustering approaches.
  - **Cluster-based recommendation engine logic** 
  - **Visualizations and metrics** exported to `results/`.
  - **Report.pdf** (academic-style writeup with methods + findings; also the final academic submission towards the fulfillment of our diploma).


## Authors
* Khushi Singh (ML Engineer, yours truly)

* Shalini Mitra (Business Intelligence Analyst, Project Architect)

This project was completed as part of our **PG Diploma in Big Data Analytics** at **CDAC-Noida (India)**.  

💡 *Why this project?*  
We chose **customer segmentation** because it merges our backgrounds: Shalini brought business intuition and logic, while I had experience tailoring conservation giving programs for diverse client profiles.  
Understanding **clusters + customer behaviour and nuances** wasn’t just academic, it’s exactly the kind of insight that drives smarter marketing, personalized outreach, meaningful client relationships (with the bonus of cool talking points in an interview!)

*AI DISCLOSURE: Some documentation, formatting, and report structuring support was assisted by generative AI tools (Perplexity.ai). All analysis, coding, and interpretation are our own.*
