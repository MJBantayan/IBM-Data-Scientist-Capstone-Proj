![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat&logo=python&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=flat)
![Seaborn](https://img.shields.io/badge/Seaborn-3776AB?style=flat)
![Plotly](https://img.shields.io/badge/Plotly-3F4F75?style=flat&logo=plotly&logoColor=white)
![Folium Badge](https://img.shields.io/badge/Folium-77B829?logo=folium&logoColor=fff&style=for-the-badge)
![Dash](https://img.shields.io/badge/Dash-0081CB?style=flat&logo=plotly&logoColor=white)
![Looker Studio](https://img.shields.io/badge/Looker%20Studio-4285F4?style=flat&logo=googlecloud&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)

# Winning the Space Race with Data Science

This project analyzes and predicts the outcome of SpaceX Falcon 9 rocket launches. Understanding which factors drive a successful landing is central to reducing launch costs, since a landed and reused first stage is far cheaper than an expendable one. The analysis combines API and web-scraped launch data, exploratory analysis in SQL and Python, interactive geospatial and dashboard visualizations, and a set of classification models trained to predict landing outcomes from mission parameters.

<img width="1515" height="661" alt="Deck-Title" src="https://github.com/user-attachments/assets/2fd0dbb5-23d3-48c8-8800-0c6f6655bca0" />

## Problem Statement

The project set out to answer three questions: which launch characteristics most influence a successful landing, whether historical data can accurately predict the outcome of a future launch, and which classification model performs best for this prediction task.

## Key Findings

Launch site, payload mass, and booster type emerged as the strongest factors influencing landing success. KSC LC-39A was the top-performing launch site, accounting for 41.7 percent of all successful launches and posting a 76.9 percent success rate for launches from that pad. All booster types contributed to successful landings across payload ranges, but FT boosters were linked to the largest share of failures in the mid-weight payload range of roughly 2,500 to 7,500 kg. Among the highest-performing booster types, FT and B5, success rates were noticeably higher for payloads above 1,500 kg, suggesting SpaceX's later hardware handles heavier missions more reliably than lighter ones. Launch success also trended upward year over year from 2013 onward, peaking around 2019, reflecting the maturing reliability of SpaceX operations.

## Approach

Data collection started with a call to the SpaceX REST API, whose JSON response was normalized into a pandas DataFrame using fields such as rocket name, payload mass, launch site, and landing outcome. This was supplemented by scraping the SpaceX Falcon 9 launch history from Wikipedia with requests and BeautifulSoup to capture fields not available through the API, such as booster versions and landing outcomes, using pandas' read_html to convert the parsed tables into DataFrames.

The API and scraped data were then combined and wrangled: columns were renamed for clarity, missing values were handled, data types were standardized, and derived features such as launch outcome and payload mass were engineered. The cleaned data was loaded into a SQLite database, and exploratory data analysis was performed both through pandas and matplotlib and seaborn visualizations and through direct SQL queries, covering unique launch sites, payload totals by customer, average payload by booster version, first successful ground landing, and landing outcome counts by year.

Geospatial patterns were explored by building an interactive Folium map that plots each launch site, color-codes launches by outcome, and marks proximity to coastlines, railroads, and the nearest city. A companion Plotly Dash application was built to let a user filter launches by site and payload range, view a pie chart of success distribution, and inspect a scatter plot of payload mass against launch outcome colored by booster version.

For prediction, four classification models were trained and tuned: Logistic Regression, Support Vector Machine (RBF kernel), Decision Tree, and K-Nearest Neighbors. Each was tuned with GridSearchCV using 10-fold cross-validation and evaluated on a held-out test set with accuracy scores and confusion matrices.

## Results

| Model | Test Accuracy | Validation Accuracy |
| --- | --- | --- |
| Logistic Regression | 83.3% | 83.3% |
| Support Vector Machine (RBF) | 83.3% | 83.3% |
| Decision Tree | 83.3% | 87.5% |
| K-Nearest Neighbors | 83.3% | 83.3% |

All four models reached the same 83.3 percent test accuracy, but the Decision Tree achieved the highest validation accuracy at 87.5 percent, with its best configuration using entropy criterion, log2 max features, and a max depth of 4. Its confusion matrix shows it correctly identified all 12 successful launches in the test set (perfect recall on the positive class), with 3 failed launches misclassified as successes and no false negatives. Logistic Regression remains the most interpretable option if transparency and speed are the priority, while the Decision Tree offers a slight edge when validation performance and decision-rule clarity matter more.

## Project Structure

The analysis is organized as a sequence of Jupyter notebooks plus a standalone dashboard script:

- `001-jupyter-labs-spacex-data-collection-api.ipynb` – collects launch data from the SpaceX REST API
- `002-jupyter-labs-webscraping.ipynb` – scrapes supplementary launch data from Wikipedia
- `003-labs-jupyter-spacex-data-wrangling.ipynb` – combines, cleans, and engineers features from the collected data
- `004-jupyter-labs-eda-sql-coursera_sqllite.ipynb` – exploratory data analysis using SQL queries against a SQLite database
- `005-edadatavizz.ipynb` – exploratory data analysis using matplotlib, seaborn, and pandas visualizations
- `006-lab_jupyter_launch_site_location.ipynb` – interactive Folium map of launch sites and proximity features
- `spacex-dash-app.py` – Plotly Dash application for interactively exploring launch outcomes by site and payload
- `008-SpaceX_Machine_Learning_Prediction_Part_5.ipynb` – model training, hyperparameter tuning, and evaluation

## Getting Started

Clone the repository and install the required Python packages, then run the notebooks in numerical order to reproduce the analysis from data collection through modeling.

```
pip install pandas numpy matplotlib seaborn plotly dash requests beautifulsoup4 scikit-learn folium sqlalchemy ipython-sql
```

To launch the interactive dashboard locally:

```
python spacex-dash-app.py
```

Then open the local address printed in the terminal to explore launch outcomes by site and payload range.

## Conclusion

Launch site, payload mass, and booster type are the clearest drivers of Falcon 9 landing success in this dataset. KSC LC-39A stands out as SpaceX's most reliable launch pad, heavier payloads above roughly 1,500 kg are handled more effectively by the newer FT and B5 boosters, and a tuned Decision Tree can forecast landing outcomes from mission parameters with meaningfully better validation accuracy than the other models tested. These findings point toward launch site selection and booster version as practical levers for improving landing reliability and, by extension, reducing the cost of each mission.

## Acknowledgments

This project was completed as part of the IBM Data Science Professional Certificate capstone, "Winning Space Race with Data Science," using SpaceX Falcon 9 launch data from the SpaceX REST API and Wikipedia.
