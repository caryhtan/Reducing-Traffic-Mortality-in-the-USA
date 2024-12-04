# Reducing Traffic Mortality in the USA
![Traffic Accidents](car-accident.jpg)

Welcome to my project on exploring strategies to reduce traffic-related fatalities in the United States! Despite significant improvements since the 1980s, the number of traffic-related fatalities has stagnated in recent years, with a concerning rise in fatal accidents. In this analysis, I explored patterns in road accidents using data from various sources to identify actionable insights for targeted interventions. I used Python and Jupyter Notebook to perform this analysis.

## View the Notebook
You can check out the full analysis here: [View Notebook](https://github.com/caryhtan/Reducing-Traffic-Mortality-in-the-USA/blob/main/notebook.ipynb)

## What I Did
I focused on answering the following key questions:
- What patterns exist in traffic accidents across different states?
- How do factors like speeding, alcohol influence, and driver history relate to fatal accidents?
- How can states be grouped to prioritize targeted interventions?

### Data Sources
I used the following datasets:
1. **data/fatal_accidents.csv**  
   This CSV file contains data on the number of fatal accidents and related features by state.
   - **`state`**: name of the state
   - **`fatal_accidents`**: number of fatal accidents
   - **`speeding`**: percentage of accidents involving speeding
   - **`alcohol`**: percentage of accidents involving alcohol
   - **`not_previously_involved`**: percentage of accidents involving first-time offenders

2. **data/miles_driven.tsv**  
   This is a TSV file containing data on the total number of miles driven in each state.
   - **`state`**: name of the state
   - **`miles_driven`**: total number of miles driven in the state (in billions)

## What I Found
Here are some key insights I discovered:
- **Patterns in Fatal Accidents**: Alcohol influence is weakly correlated with the number of fatal accidents, but it shows strong associations with other factors like speeding.
- **State Clusters**: States can be grouped into three distinct clusters based on speeding, alcohol influence, and first-time offenders.
- **Cluster Prioritization**: Clusters with higher total fatal accidents may require immediate attention for interventions.

## How I Did It
To answer these questions, I:
1. Loaded datasets from CSV and TSV files using `pandas`.
2. Performed exploratory data analysis, including calculating summary statistics and creating scatter plots.
3. Used Principal Component Analysis (PCA) to reduce dimensions and visualize state groupings.
4. Applied KMeans clustering to identify clusters of states with similar accident profiles.
5. Visualized feature differences and total fatal accidents within clusters to prioritize interventions.

### Example Code
Here’s an example of the code I used:
```python
# Standardize features for PCA
from sklearn.preprocessing import StandardScaler
scaled_data = StandardScaler().fit_transform(accidents_df[['speeding', 'alcohol', 'not_previously_involved']])

# Perform PCA
from sklearn.decomposition import PCA
pca = PCA(n_components=2)
principal_components = pca.fit_transform(scaled_data)

# Add PCA results to the DataFrame
accidents_df['PCA1'] = principal_components[:, 0]
accidents_df['PCA2'] = principal_components[:, 1]
