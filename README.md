![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat&logo=python&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=flat)
![Seaborn](https://img.shields.io/badge/Seaborn-3776AB?style=flat)
![Plotly](https://img.shields.io/badge/Plotly-3F4F75?style=flat&logo=plotly&logoColor=white)
![Dash](https://img.shields.io/badge/Dash-0081CB?style=flat&logo=plotly&logoColor=white)
![Looker Studio](https://img.shields.io/badge/Looker%20Studio-4285F4?style=flat&logo=googlecloud&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)

This project aims to analyze and predict the key factors influencing successful landings of the Falcon 9 rockets, which is critical for reducing costs and improving the reusability of rockets.

We identified that the factors influencing the successful landing of rockets are launch site, payload mass and booster type. KSC LC-39A emerged as the top performing launch site contributing to 76.9% of successful launches. While all booster types contributed greatly to successful launches and landing, FT boosters contributed to most failures in the mid-range payload mass. For the most high performing boosters, FT and B5 there is a noticeable higher success rate for payloads above 1500Kg. 
Approach

The project started with a call to SpaceX REST API which yielded a JSON file that I saved into a Pandas dataframe. Then I scraped data and saved them to a database. After data wrangling I performed EDA by querying the SQLite database. I visualized the geodata with Folium and the launch data with Dash. Tested multiple ML algos where the Decision Tree model achieved the highest validation accuracy at 87.5%, correctly identifying all successful launches per the mission parameters. 
