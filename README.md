# Ball is Life? Statistical Analysis of American Cross-Cultural Versus Match Engagement During the 2026 World Cup
All code written and polished for a Dartmouth College QSS020 final project, Summer 2026. This README functions as a guide to run and recreate all steps of the project. The bulk of the data scraping was performed in the first notebook. The second notebook functions as a cleaning script. The third and fourth notebooks analyze and visualize all cleaned data.
# Order to Run
1. [0_pull_format_all_api_data.ipynb](https://github.com/loganjeskildsen28/qss20_final_project/code/0_pull_format_all_api_data.ipynb)
- Inputs:
    - A header required to make requests to the MediaWiki API via the pywikibot library, see documentation here: (https://doc.wikimedia.org/pywikibot/master/)
    - The Pytrends wrapper library to make requests to an unofficial Google Trends API, see documentation here: (https://pypi.org/project/pytrends/)

- Function of this Document:
    - Creates a basic DataFrame on relevant details for countries that faced off against the U.S in 2026. Contains match type, year played, outcome, score, and match date for each country. Diagnostics included when printing DataFrames.
    - Scrapes for all Wikipedia subcategories per country and all Wikipedia articles per subcategory using pywikibot.
    - Scrapes daily article viewcount from each article in the most popular subcategories and the main country page. Returns a dataframe with over 110,000 records.
    - Uses the pytrend library to call for cultural versus match search trends over 11 U.S. host cities and a non-host city control. Returns a DataDrame that shows weekly proportion of cultural versus match related searches over the relevant World Cup windows.

- Key Outputs:
    - Saves dirty dataframes to callable .csv files in the data folder of this repository for future use. Listed below:
        - [basic_info.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/basic_info.csv)
        - [article_views.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/article_views.csv)
        - [country_article_views.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/country_article_views.csv)
        - [football_article_views.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/football_article_views.csv)
        - [regional_search_interest.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/regional_search_interest.csv)


2. [1_clean_merge_data.ipynb](https://github.com/loganjeskildsen28/qss20_final_project/code/1_clean_merge_data.ipynb)
- Inputs:
    - [0_pull_format_all_api_data.ipynb](https://github.com/loganjeskildsen28/qss20_final_project/code/0_pull_format_all_api_data.ipynb)

- Function of this Document:
    - Reads all relevant dirty .csv files and converts to pandas DataFrame objects with proper datetime format.
    - Filters the article_views DataFrame into the culture_views DataFrame by selecting for articles with subcategories that begin with "History of," "Society of," and "Culture of."
    - Separates Wikipedia DataFrames into baseline data (5/17/2026-5/26/2026) and main data (5/27/2026-8/20/2026). Calculates mean and standard deviation of daily pageviews for each article.
    - Performs left joins of the main DataFrame with basic_info_df and baseline statistics on 'country' and ['country', 'article_title'] respectively. Six left joins performed total.
    - Performs left joins of the search trends DataFrame with a DataFrame of listed host cities on the Google Trends geo codes for each city.

- Key Outputs:
    - [culture_final_data.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/culture_final_data.csv)
    - [football_final_data.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/culture_final_data.csv)
    - [country_final_data.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/culture_final_data.csv)
    - [regional_final_data.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/culture_final_data.csv)


3. [2_visualize_wikipedia_outputs.ipynb](https://github.com/loganjeskildsen28/qss20_final_project/code/2_visualize_wikipedia_outputs.ipynb)
- Inputs:
    - Wikipedia .csv outputs from [1_clean_merge_data.ipynb](https://github.com/loganjeskildsen28/qss20_final_project/code/1_clean_merge_data.ipynb)

- Function of this Document:
    - Plots timeseries of main pageviews as a ratio to the baseline mean for each country using for loops
          - Repeated for culture, football, and country data
    - Uses SciPy library to fit an exponential decay curve to pageview data starting from peak pageviews after the matchup against the U.S..
    - Generates statistics on half lives of decay curves, difference of half lives of football and culture decay curves.
    - Finds proportion of excess pageviews 7 days after the match by 1) country and subcategory type, 2) country article with the largest share of excess views and plots in a regression coefficient style plot.

- Key Outputs:
    - [figure_1.png](https://github.com/loganjeskildsen28/qss20_final_project/outputs/figure_1.png)
    - [figure_2.png](https://github.com/loganjeskildsen28/qss20_final_project/outputs/figure_2.png)
    - [figure_3.png](https://github.com/loganjeskildsen28/qss20_final_project/outputs/figure_3.png)
    - [figure_4.png](https://github.com/loganjeskildsen28/qss20_final_project/outputs/figure_4.png)
    - [figure_5.png](https://github.com/loganjeskildsen28/qss20_final_project/outputs/figure_5.png)

4. [3_visualize_google_trends_outputs.ipynb](https://github.com/loganjeskildsen28/qss20_final_project/code/3_visualize_google_trends_outputs.ipynb)
- Inputs:
    - Google Trends .csv output [regional_final_data.csv](https://github.com/loganjeskildsen28/qss20_final_project/data/culture_final_data.csv) from [1_clean_merge_data.ipynb](https://github.com/loganjeskildsen28/qss20_final_project/code/1_clean_merge_data.ipynb)

- Function of this Document:
    - Combines initial cultural and match keyword proportions into global cultural and match interest
    - Uses a for-loop for 11 host cities + Chicago to plot np.log1p of cultural and match interest per country.
    - Draws World Cup vertical bars to indicate cup window on plots.

- Key Outputs:
    - [figure_6.png](https://github.com/loganjeskildsen28/qss20_final_project/outputs/figure_6.png)




