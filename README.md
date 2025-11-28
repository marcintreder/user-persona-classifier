# Unsupervised Discovery of Mobile User Personas for UX Strategy

## Project Overview
I work as a UX Director at Google and I often encounter user segments defined by rigid demographics (e.g., "iOS Users" vs. "Android Users"). This project challenges those assumptions by applying **Unsupervised Machine Learning** to discover latent user personas based purely on behavioral data.

Using a dataset of mobile usage metrics, I employed **K-Means Clustering** and **Hierarchical Clustering** to identify natural groupings in the data. The analysis revealed that user behavior is driven by **usage intensity**, not device platform, providing actionable insights for product strategy.

## he Dataset
**Source:** [Mobile Device Usage and User Behavior Dataset (Kaggle)](https://www.kaggle.com/datasets/valakhorasani/mobile-device-usage-and-user-behavior-dataset)

The dataset contains 700 records of user behavior. For this unsupervised learning project, the existing labels were removed to allow the model to discover patterns organically.

**Key Features:**
* **App Usage Time (min/day):** Time spent inside applications.
* **Screen On Time (hours/day):** Total active screen duration.
* **Battery Drain (mAh/day):** Daily battery consumption.
* **Data Usage (MB/day):** Mobile data consumed.
* **Operating System:** Categorical (Android/iOS).

---

## Methodology
The project follows a rigorous data science workflow:

### 1. Exploratory Data Analysis (EDA)
* **Multicollinearity:** Discovered extreme correlations (>0.95) between Screen Time, Battery Drain, and Data Usage.
* **OS Split:** Visualized the class imbalance (Android majority) but confirmed via Violin Plots that usage distributions were similar across platforms.
* **Outlier Check:** Confirmed the dataset was clean with no significant outliers requiring removal.

### 2. Preprocessing & Dimensionality Reduction
* **Scaling:** Applied `StandardScaler` to normalize features with vastly different magnitudes (e.g., mAh vs. Hours).
* **Encoding:** Applied `OneHotEncoder` to the 'Operating System' feature.
* **PCA (Principal Component Analysis):** Reduced the dataset to **2 Principal Components** (explaining 96% of the variance) to address multicollinearity and allow for 2D visualization.

### 3. Model Building & Comparison
Two distinct unsupervised algorithms were trained and compared:
* **Model 1: K-Means Clustering**
    * Optimized $k$ using the **Elbow Method** and **Silhouette Analysis**.
    * Result: $k=3$ was chosen as the optimal balance between cohesion and interpretability.
* **Model 2: Hierarchical Clustering (Agglomerative)**
    * Optimized using **Linkage Analysis** (Ward vs. Complete vs. Average).
    * Result: Ward Linkage produced a tree that naturally split into 3 distinct branches.

---

## Key Findings & Personas

The analysis identified **3 distinct user personas** that cut across operating systems:

| Persona | Screen Time | Battery Drain | UX Profile |
| :--- | :--- | :--- | :--- |
| **The Minimalist** | ~2.3 Hours | ~680 mAh | Utility-focused. Low engagement. Needs streamlined UI. |
| **The Standard User** | ~6.0 Hours | ~1800 mAh | The "Average" user. Balances utility and entertainment. |
| **The Power User** | >10 Hours | ~2700 mAh | Extreme engagement. Heavy data/battery usage. Needs "Dark Mode" & Data Saver. |

### Strategic Insight
A major finding of this project is **Platform Independence**.
* PCA visualization revealed that while iOS and Android users are mathematically distinct (due to encoding), **all three personas exist in equal proportions across both platforms**.
* **Conclusion:** "Power Users" are platform-agnostic. Product features should target *behavior*, not *device*.

---

## Technologies Used
* **Python 3.10**
* **Pandas & NumPy:** Data manipulation.
* **Scikit-learn:** PCA, K-Means, Preprocessing pipelines, Silhouette metrics.
* **SciPy:** Hierarchical clustering and Dendrograms.
* **Seaborn & Matplotlib:** Data visualization.
* **Google Colab:** Development environment.

## 🚀 How to Run
1.  Clone the repository:
    ```bash
    git clone [https://github.com/YOUR_USERNAME/mobile-user-behavior-segmentation.git](https://github.com/YOUR_USERNAME/mobile-user-behavior-segmentation.git)
    ```
2.  Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```
3.  Open the notebook:
    ```bash
    jupyter notebook notebooks/msai_mobile_user_behavior.ipynb
    ```
    *(Note: You will need a Kaggle API key to download the dataset dynamically, or manually place the CSV in the directory.)*
