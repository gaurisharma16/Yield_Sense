# 🌾 Yield Sense: Comparative Climate Risk & Agricultural Forecasting Simulator

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?logo=streamlit&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Random%20Forest%20%7C%20Gradient%20Boosting-success)

**Yield Sense** is an end-to-end machine learning pipeline and interactive scenario simulator designed to predict wheat yields and assess climate risk across India and the United States. 

By bridging the gap between historical agricultural momentum and localized climate shocks, this tool empowers researchers, policymakers, and agriculturists to actively simulate "What-If" drought and heatwave scenarios, transforming static historical data into a dynamic tool for global food security planning.

---

## 🌍 The Problem

Global agriculture faces unprecedented volatility due to climate change. Traditional crop forecasting methods often rely on simple historical averages. However, these baseline models fail to account for the devastating impact of sudden climate anomalies—such as a late-season heatwave or severe rainfall deficit. 

Furthermore, crop survival depends on complex biological interactions (e.g., heat is survivable with high moisture, but fatal during a drought). Policymakers need tools that do not just look at "average weather," but quantify the **shock** and its direct impact on the harvest.

## 💡 The Solution

**Yield Sense** solves this by engineering domain-specific biological features to model how crops react to stress. We utilized decades of localized district/county-level data to train complex tree-based ensemble models. Finally, the models are deployed via a **Streamlit Dashboard** that allows users to adjust weather variables in real-time, instantly calculating the projected yield impact of an impending climate crisis.

---

## 🔬 Methodology & Pipeline Architecture

The project is structured into four distinct phases:

### Phase 1: Comparative Exploratory Data Analysis (EDA)
We conducted a deep comparative analysis of agricultural trends in India and the USA, mapping out:
* **Yield Volatility:** Identifying which specific states/districts are "high-risk" and prone to boom-and-bust harvest cycles.
* **The Danger of Terminal Heat:** Visualizing the severe negative correlation between late-season temperature spikes and final harvest weights.
* **Agricultural Momentum:** Plotting the 3-year rolling means to establish the baseline infrastructure and soil quality of every individual district.

### Phase 2: Domain-Specific Feature Engineering
Raw weather data is insufficient for predicting biological outcomes. We engineered features to simulate real-world crop stress:
* **Momentum Features:** `Yield_Rolling_Mean3` and `Yield_Rolling_Std3` establish the historical baseline and volatility of a region.
* **Climate Shocks:** `Temperature_Anomaly` and `Rainfall_Deviation` calculate how much the current season deviates from that specific district's historical norm.
* **Biological Ratios:** * `Terminal_vs_AvgTemp`: Isolates sudden heat spikes during the critical grain-filling stage.
  * `Rain_per_Temp`: A proxy for moisture efficiency, measuring if there was enough rain to offset evaporative heat demand.
  * `SowingRain_to_TotalRain`: Tracks the timing of moisture delivery for seed germination.

### Phase 3: Model Selection & Training
Machine learning algorithms were tailored to the specific climatic behaviors of each country. To allow the models to understand geography, we utilized strict **One-Hot Encoding (OHE)** for States and Districts, saving the exact dimensional metadata to ensure seamless deployment.
* **India Model (Gradient Boosting Regressor):** Chosen for its ability to handle the highly non-linear relationships of the Indian monsoon and varying irrigation access.
* **USA Model (Random Forest Regressor):** Chosen for its robustness against overfitting to outlier years, creating a highly stable "wisdom of the crowd" prediction across diverse US geographies.

### Phase 4: Streamlit Deployment & Scenario Simulation
The trained `.pkl` models and OHE metadata were deployed into an interactive Python frontend. The app:
1. Loads the historical baseline weather for a user-selected district.
2. Allows the user to manipulate sliders (e.g., increase temperature by 2°C).
3. Automatically calculates the *new* engineered anomalies in the background.
4. Feeds the aligned tensor into the model to predict the final Yield in real-time.

---

## 📊 Model Performance

Our models move beyond simply guessing the mean, accurately penalizing the yield when fed extreme weather parameters.

| Country | Algorithm | Accuracy (R² Score) | Target Variable |
| :--- | :--- | :--- | :--- |
| **India** | Gradient Boosting Regressor | **~87.8%** | Yield (Kg/Hectare) |
| **USA** | Random Forest Regressor | **~86.0%** | Yield (Kg/Hectare) |


```bash
git clone [https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git](https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git)
cd YOUR_REPOSITORY_NAME
