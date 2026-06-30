Zomato wants to better understand its restaurant ecosystem in Hyderabad in order to improve customer experience and support business decisions for restaurant partners. This project analyzes restaurant metadata and ~10,000 customer reviews to:


Discover natural restaurant segments (clusters) based on cost, cuisine, ratings, and review text — without any predefined labels.
Understand customer sentiment from written reviews — what drives happy vs. unhappy experiences.
Surface actionable business insights — does price correlate with quality? Which cuisines underperform? When should marketing campaigns run?


This is an unsupervised learning problem: there's no "correct" restaurant category already given in the data — the model has to discover hidden structure on its own, similar to how a retailer might segment customers without anyone telling it the segments in advance.


📊 Dataset

FileRowsDescriptionZomato_Restaurant_names_and_Metadata.csv105Restaurant name, cost, cuisines, Zomato collections, timingsZomato_Restaurant_reviews.csv10,000Reviewer, review text, star rating, timestamp, photos


🔍 What This Project Does

1. Data Cleaning & Wrangling


Fixed cost column (stored as text with commas)
Removed invalid rating entries (non-numeric "Like" values)
Parsed timestamps, engineered features like cuisine count, review length, reviewer experience


2. Exploratory Data Analysis (15 charts)
Following the UBM rule — Univariate, Bivariate, and Multivariate analysis — covering rating distribution, cost patterns, review activity over time, cuisine-level sentiment, and more. Every chart includes a written explanation of why it was chosen, what insight it reveals, and its business impact.

3. Hypothesis Testing
Three statistically tested hypotheses using Pearson correlation and Welch's t-test:


Does cost correlate with rating? → Yes, significant (p < 0.001)
Does cuisine variety affect rating? → Not significant
Does weekday vs. weekend posting affect rating? → Not significant


4. NLP & Feature Engineering


Full text preprocessing pipeline: contraction expansion, lowercasing, punctuation/URL removal, stopword removal, stemming, tokenization
TF-IDF vectorization of review text per restaurant
Dimensionality reduction via Truncated SVD
Structured features scaled and combined with text features into a single feature matrix


5. Machine Learning — Clustering
Three models built, evaluated, and hyperparameter-tuned:

ModelTechniqueWhy UsedKMeansCentroid-basedFast, interpretable baselineAgglomerative HierarchicalBottom-up merging (Ward linkage)No shape assumption, dendrogram visualizationDBSCANDensity-basedAuto-detects cluster count + outliers

Each model evaluated using Silhouette Score, Davies-Bouldin Index, and Calinski-Harabasz Index, with hyperparameters tuned via grid search.

6. Business Outcome
Final tuned KMeans model segments restaurants into actionable groups, e.g.:


Premium Dining (higher cost, higher rating, high positive sentiment)
Popular Budget Eats (lower cost, high review volume)
Struggling Restaurants (low rating, low engagement — flagged for intervention)



🛠️ Tech Stack


Python, Pandas, NumPy — data manipulation
Matplotlib, Seaborn — visualization
Scikit-learn — TF-IDF, scaling, PCA/SVD, KMeans, Agglomerative, DBSCAN, evaluation metrics
SciPy — statistical hypothesis testing
Joblib — model persistence



📁 Repository Structure

├── Zomato_Capstone_Final.ipynb              # Main notebook (run this)
├── Zomato_Restaurant_names_and_Metadata.csv # Restaurant metadata
├── Zomato_Restaurant_reviews.csv            # Customer reviews
└── README.md


▶️ How to Run


Clone or download this repository
Make sure all 3 files (notebook + 2 CSVs) are in the same folder
Open Zomato_Capstone_Final.ipynb in Jupyter Notebook
Run All cells (Kernel → Restart & Run All)


No additional setup required beyond standard pandas, numpy, matplotlib, seaborn, scikit-learn, and scipy.


📈 Key Business Recommendations


Feature high-rated, high-volume restaurants prominently to build platform trust
Promote a "value for money" discovery category for budget-conscious users
Schedule review-prompt notifications around weekend evening peak hours
Flag restaurants in the low-performing cluster for partner quality review
Monitor cuisines with above-average negative sentiment for early intervention
