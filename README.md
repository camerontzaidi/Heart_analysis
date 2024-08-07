# Interconnections of Lifestyle and Health: A Data-Driven Approach to Heart Disease, Stroke, and Diabetes

This project employs the Behavioral Risk Factor Surveillance System (BRFSS) 2015 dataset to develop predictive models targeting heart disease, strokes, and diabetes. The primary objective is to identify key factors that contribute to the risk of these health conditions.

## Overview
Heart disease remains the primary cause of mortality in the United States. Early detection and preventive measures are crucial due to the typically asymptomatic progression of heart disease until critical symptoms manifest.

Leveraging a custom-built application developed using Python and Streamlit, this study integrates statistical analysis with machine learning techniques to dissect the relationship between various risk factors and the prevalence of heart disease, stroke, and diabetes. The application facilitates interactive data visualization and analysis, allowing users to dynamically explore data and uncover significant health predictors.

## Data
The BRFSS 2015 dataset consists of responses from over 400,000 Americans. After cleaning and preprocessing, the dataset was refined to focus on 253,680 responses. Key variables include:

- **High Blood Pressure (HighBP)**
- **High Cholesterol (HighChol)**
- **Cholesterol Checked (CholCheck)**
- **Body Mass Index (BMI)**
- **Smoker**
- **Stroke**
- **Diabetes**
- **Physical Activity (PhysActivity)**
- **Fruits**
- **Vegetables (Veggies)**
- **Heavy Alcohol Consumption (HvyAlcoholConsump)**
- **Healthcare Access (AnyHealthcare)**
- **Cost-Related No Doctor Visit (NoDocbcCost)**
- **General Health (GenHlth)**
- **Mental Health (MentHlth)**
- **Physical Health (PhysHlth)**
- **Difficulty Walking (DiffWalk)**
- **Sex**
- **Age**
- **Education**
- **Income**

## Methodology
### Data Cleaning
Data cleaning was an essential step to prepare the dataset for analysis.

### Application Development: Utilizing Conditional Entropy
The project employs a sophisticated application developed using Python and Streamlit, which leverages conditional entropy to analyze and visualize data relationships within the BRFSS dataset. The application includes three interconnected modules:

1. **Advanced Data Visualization**: Generates histograms, calculates covariance matrices, and visualizes data through heatmaps.
2. **Contingency Table Analysis**: Creates and visualizes contingency tables, allowing users to examine relationships between different categorical health-related variables.
3. **Conditional Entropy Calculation**: Calculates and visualizes conditional entropy for various health-related variables, helping to identify the most significant predictors of health conditions.

## Results & Discussion
### Heatmap Analysis
Heatmaps provide a visual representation of correlations between variables.

### Histogram Analysis
Histograms reveal the distribution of key factors such as age, education, and income across different conditions.

### Conditional Entropy Analysis
Conditional entropy was calculated to assess the uncertainty in heart disease occurrence given various risk factors. The analysis reveals the predictability of health conditions based on socio-economic status, age, and other factors.

## Limitations
- **Dataset Limitations**: Based on self-reported data which can introduce biases.
- **Methodological Constraints**: Conditional entropy does not quantify the strength or direction of relationships.
- **Generalizability**: Findings may not be directly generalizable to other populations.
- **Software and Implementation**: Reliance on Python and Streamlit for data processing and visualization.

## Conclusion
This study highlights the critical risk factors associated with heart disease, stroke, and diabetes. The findings underscore the significant role of socio-economic factors such as income, education, and age in influencing health outcomes. The interactive application developed facilitates the exploration and visualization of data, providing valuable insights that could lead to more effective public health strategies.

## References
1. Centers for Disease Control and Prevention. (2015). Behavioral Risk Factor Surveillance System.
2. Mathis, K. (2022, March 10). Heart disease health indicators dataset discussion. Kaggle.
3. Orlitsky, A. (n.d.). Conditional entropy. ScienceDirect Topics.
4. Teboul, A. (2022, March 10). Heart disease health indicators dataset. Kaggle.

