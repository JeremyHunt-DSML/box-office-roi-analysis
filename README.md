# The Hollywood Box Office ROI Analysis 🎬

[![View on nbviewer](https://img.shields.io/badge/Open_in-nbviewer-orange.svg)](https://nbviewer.org/github/JeremyHunt-DSML/box-office-roi-analysis/blob/main/hollywood_roi_analysis.ipynb)

A data analytics project answering the core question: does a bigger budget equal a better movie? Built using Python, Pandas, SQL, and Seaborn.

## Project Overview
This project is an end-to-end Data Engineering and Data Science ETL (Extract, Transform, Load) pipeline. It aims to answer the core financial question of the film industry: **Does spending more money on a movie guarantee better critical reception and higher box office returns?**

By extracting and merging disparate datasets from flat files, web scraping, and API connections, this project analyzes the relationship between production budgets, critic scores, age ratings, and box office profitability.

## The ETL Pipeline
1. **Extract:** * Sourced baseline metadata and financial data from a Kaggle CSV.
   * Web-scraped all-time box office rankings from Wikipedia using `BeautifulSoup`.
   * Connected to the OMDb API via a paid authentication key to fetch verified Rotten Tomatoes scores, runtimes, and MPAA age ratings.
2. **Transform:** * Performed extensive text normalization (converting to lowercase, stripping whitespace/footnotes) to create a universal `movie_title` join key.
   * Utilized Regular Expressions to clean currency formats.
   * Handled missing values and documented the ethical implications of "survival bias" regarding dropped data.
3. **Load:** * Loaded the three clean dataframes into a local SQLite database (`hollywood_project.db`).
   * Executed SQL `LEFT JOIN` commands to merge the sources into a single master dataset.

## Technologies & Libraries Used
* **Python 3**
* **Pandas** (Data manipulation and cleaning)
* **BeautifulSoup / Requests** (Web scraping)
* **OMDb API** (JSON parsing and rate-limit handling)
* **SQLite3** (Database management and SQL joins)
* **Seaborn & Matplotlib** (Data visualization)

## Key Insights
* **Budget vs. Quality:** A higher production budget does *not* guarantee critical acclaim. Low-to-medium budget films span the entire spectrum from masterpieces to disasters.
* **The Audience/Critic Divide:** Audiences (IMDb) tend to rate movies more moderately, while professional critics (Rotten Tomatoes) spread wider at the extremes, showing a clear divide in how "quality" is measured.
* **The ROI Sweet Spot:** Broadly accessible, family-friendly age ratings (PG, PG-13) consistently yield a higher average Return on Investment multiplier compared to R-rated films, which artificially restrict their target audience.

## Ethical Implications & Bias
During the data cleaning process, specific assumptions and transformations were made that introduced potential bias. By dropping rows with missing production budgets or missing Rotten Tomatoes scores, the dataset leans heavily toward mainstream, commercial Hollywood productions. Independent and foreign films are less likely to publicly report financials or be aggregated by Western critics, resulting in a survival bias within the final analysis. Furthermore, isolating Rotten Tomatoes percentages risks "Context Collapse" by stripping away the nuance of total review counts.
