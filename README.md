# Predictive Modelling Cultural Engagement After the World Cup
All code written and polished for a Dartmouth College QSS020 final project, Summer 2026. This README functions as a work in progress until 8/30/2026. The bulk of the work has been done in the first notebook to run.
# Order to Run
1. [0_pull_format_all_api_data.ipynb](https://github.com/loganjeskildsen28/qss20_final_project/code/0_pull_format_all_api_data.ipynb)
- Inputs:
    - A header required to make requests to the MediaWiki API via the pywikibot API, see documentation here: (https://doc.wikimedia.org/pywikibot/master/)
    - An API key required to make requests to the Census Bureau API, see documentation here: (https://www.census.gov/data/developers/guidance/api-user-guide.html)
    - A user-created Kaggle dataset on sentiment-scores for 22,360 tweets during the 2022 World Cup. Data link here: (https://www.kaggle.com/datasets/tirendazacademy/fifa-world-cup-2022-tweets)

- Function of this Document:
    - Creates a basic dataframe on relevant details for countries that faced off against the U.S. since 2014. Contains match type, year played, outcome, score, and match date for each country.
    - Scrapes for all Wikipedia subcategories per country using pywikibot and concatenates the four most popular subcategories to subcat_df_data.
    - Scrapes daily article viewcount from each article in the most popular subcategories and the main country page. Returns a dataframe with over 88,000 rows.
    - Takes in manually inputted country variable code data and calls a user-defined function that returns the region with the highest diaspora populations from each country using the Census Bureau API.
    - Uses the pytrend library to call for cultural versus match search trends over all U.S. media market regions. Returns a dataframe that shows proportion of cultural versus match related searches over the relevant World Cup windows.
    - Reads the installed Kaggle .csv file.

- Key Outputs:
    - Saves dirty dataframes to callable .csv files in the data folder of this repository for future use. Listed below:
        - [basic_info.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/basic_info.csv)
        - [subcategory_data.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/subcategory_data.csv)
        - [daily_wikipedia_views_all.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/daily_wikipedia_views_all.csv)
        - [country_daily_views.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/country_daily_views.csv)
        - [diaspora_2022.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/diaspora_2022.csv)
        - [diaspora_2024.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/diaspora_2024.csv)
        - [regional_search_interest.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/regional_search_interest.csv)
        - [fifa_world_cup_2022_tweets.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/fifa_world_cup_2022_tweets.csv)

2. [1_clean_merge_data.ipynb](https://github.com/loganjeskildsen28/qss20_final_project/code/1_clean_merge_data.ipynb)
- Inputs:
    - All .csv outputs from 0_pull_format_all_api_data.ipynb

- Function of this Document:
    - Reads all relevant dirty .csv files and converts to pandas DataFrame objects.

- Key Outputs:
    - [cleaned_wikipedia_data.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/cleaned_wikipedia_data.csv)
    - [total_wikipedia_dataset.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/total_wikipedia_dataset.csv) used in 4_predictive_engagement_model.ipynb as complete dataset

3. [2_visualize_wikipedia_outputs.ipynb](https://github.com/loganjeskildsen28/qss20_final_project/code/2_visualize_wikipedia_outputs.ipynb)
- Inputs:
    - Cleaned wikipedia data from 1_clean_merge_data.ipynb.

- Function of this Document:
    - Visualizes viewcount 
    - WORKING Compares half-lives of engagement based on different parameters (score differential, match type, historical rivarly)

- Key Outputs:
    - TBD

4. [3_visualize_regional_and_sentiment.ipynb](https://github.com/loganjeskildsen28/qss20_final_project/code/0_pull_format_all_api_data.ipynb)
- Inputs:
    - Still deciding relevance of this notebook. All TBD

- Function of this Document:
    - TBD

- Key Outputs:
    - TBD

5. [4_predictive_engagement_model.ipynb](https://github.com/loganjeskildsen28/qss20_final_project/code/4_predictive_engagement_model.ipynb)
- Inputs:
    - (https://github.com/loganjeskildsen28/qss20_final_project/data/total_wikipedia_dataset.csv)
    - The sklearn library

- Function of this Document:
    - TO BE ADDED Applies a Random Forest Regressor to scraped Wikipedia dataset on daily pageviews during respective World Cups [in this repo](https://github.com/loganjeskildsen28/qss20_final_project/data/daily_wikipedia_views_all.csv)

- Key Outputs:
    - A predictive model that predicts engagement via wikipedia page views within (x%) RMSE


