This project aims to analyze and predict the key factors influencing successful landings of the Falcon 9 rockets, which is critical for reducing costs and improving the reusability of rockets.

We identified that the factors influencing the successful landing of rockets are launch site, payload mass and booster type. KSC LC-39A emerged as the top performing launch site contributing to 76.9% of successful launches. While all booster types contributed greatly to successful launches and landing, FT boosters contributed to most failures in the mid-range payload mass. For the most high performing boosters, FT and B5 there is a noticeable higher success rate for payloads above 1500Kg. 
Approach

The project started with a call to SpaceX REST API which yielded a JSON file that I saved into a Pandas dataframe. Then I scraped data and saved them to a database. After data wrangling I performed EDA by querying the SQLite database. I visualized the geodata with Folium and the launch data with Dash. Tested multiple ML algos where the Decision Tree model achieved the highest validation accuracy at 87.5%, correctly identifying all successful launches per the mission parameters. 
