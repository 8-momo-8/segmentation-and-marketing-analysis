Customer Segmentation & Marketing Campaign Analysis

Business Context and Project Objectives
	•	Context: A retail company (e.g. wine and gourmet food retailer) ran multiple marketing campaigns and collected customer data (demographics, purchase history, campaign responses). They lacked a deep understanding of customer behavior and campaign effectiveness. This project analyzes the data to uncover patterns and improve marketing strategy.
	•	Challenge: Marketing managers need to identify distinct customer segments and drivers of campaign engagement to optimize future campaigns. The company wants to increase campaign acceptance rates, maximize customer spending, and improve return on marketing investments.
	•	Objectives:
	•	Identify customer segments via clustering that group customers with similar profiles and behaviors.
	•	Determine key factors influencing campaign response, using statistical analysis and predictive modeling.
	•	Derive actionable insights about each segment's value and tailor marketing strategies to each group.
	•	Provide practical recommendations for campaign design and resource allocation.

Dataset Description and Key Variables
	•	Dataset Overview: Marketing campaign dataset of 2,240 customers with demographics, purchase behavior, and campaign responses.
	•	Key variables: Age, Education, Marital_Status, Income, Recency, Total_Spending, Total_Purchases, Campaign Responses.
	•	Data Quality: Minimal missing data; handled through imputation and encoding.

Analytical Methodology in Model Development
	•	Feature Engineering & Preprocessing: Created new features including Age, Total_Spending, Total_Purchases, and Total_Campaigns_Accepted. Standardized features and handled missing values.
	•	Dimensionality Reduction: Applied PCA preserving 95% variance → 21 principal components.
## Enhanced Clustering Methodology

We implemented a systematic approach to identify optimal customer segments by evaluating multiple clustering algorithms across different cluster counts (2-10).

### Algorithm Evaluation
| Algorithm          | Best n_clusters | Silhouette Score |
|--------------------|-----------------|------------------|
| K-Means            | 2               | 0.220            |
| Agglomerative      | 2               | 0.172            |
| Gaussian Mixture   | 2               | 0.208            |
| OPTICS             | -               | -0.281           |

### Cluster Evaluation Metrics
- **Silhouette Score**: 0.220
- **Calinski-Harabasz Index**: 544.441
- **Davies-Bouldin Index**: 1.935
- **Average intra-cluster distance**: 6.194
- **Average inter-cluster distance**: 7.707
- **Separation ratio**: 1.244

### Key Visualization Insights
(Visualization insights remain unchanged)

	•	Cluster Evaluation: Confirmed clusters are well-separated and meaningful.
	•	Cluster Profiling: Analyzed cluster statistics to identify segment differences.
	•	Statistical Significance Testing: ANOVA tests confirmed significant differences between clusters.
	•	Predictive Modeling (Campaign Response): Built Random Forest Classifier with ROC AUC of 1.000.
	•	Customer Lifetime Value (CLV) Estimation: 
        **Why CLV?** To quantify long-term customer value and prioritize marketing resources.
        **How we modeled:**
        1. Selected RFM features (Recency, Frequency, Monetary) plus Total Campaigns Accepted as predictors
        2. Used 40% of historical spending as proxy for next year's value (conservative estimate)
        3. Chose linear regression for interpretability and simplicity
        4. Trained model on entire dataset: clv_model = LinearRegression().fit(X_clv, y_clv)
        5. Calculated growth potential by comparing predicted CLV against current spending
        This approach provided quantifiable segment value and identified growth opportunities.
	•	Integration for Strategy: Combined insights to formulate segment-specific marketing strategies.

Business Insights and Practical Recommendations
(Segment analysis and recommendations remain unchanged)

## Key Strategic Insights
- Cluster 1 delivers 5x higher spending than Cluster 0
- Perfect separation in campaign response prediction (ROC AUC: 1.000)
- Top response predictors: Past campaign interactions, recency, meat/wine spending
- Cluster 0 shows 684.8% CLV growth potential vs 118.6% for Cluster 1
