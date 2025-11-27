
# IMDB Top 50 Movies - Data Scraping and Exploratory Data Analysis (EDA)

This notebook demonstrates a complete workflow for scraping movie data from IMDB's 'Top 50 Movies' chart, performing basic data preprocessing, and conducting an exploratory data analysis (EDA) to understand the dataset's characteristics.

## 1. Data Scraping

-   **Objective**: Extract information about the top movies (Title, Year, Rating, Rank) from the IMDB website.
-   **Tools**: `requests` for fetching the web page content and `BeautifulSoup` for parsing the HTML.
-   **Process**:
    1.  The `requests` library is used to send an HTTP GET request to `https://www.imdb.com/chart/top/`.
    2.  `BeautifulSoup` is then used to parse the HTML content.
    3.  A loop iterates through the list items on the page, specifically targeting elements containing movie details.
    4.  For each movie, the Title, Year, and Rating are extracted. A Rank is assigned based on the iteration order.
    5.  The extracted data is stored in a dictionary named `movie_data`.

## 2. Data Preprocessing

-   **Objective**: Clean and transform the scraped data into a structured format suitable for analysis.
-   **Tools**: `pandas` library.
-   **Process**:
    1.  The `movie_data` dictionary is converted into a pandas DataFrame `df`.
    2.  The 'Rating' and 'Year' columns are converted to numeric types using `pd.to_numeric`. `errors='coerce'` is used to handle any non-numeric values gracefully by converting them to `NaN`.
    3.  The processed DataFrame is saved to a CSV file named `scraped_movies.csv`.

## 3. Exploratory Data Analysis (EDA)

This section performs a comprehensive EDA to gain insights into the dataset.

### Data Structure Exploration

-   The dataset contains 25 rows and 4 columns: 'Title' (object), 'Year' (float64), 'Rating' (float64), and 'Rank' (int64).
-   Memory usage is approximately 2.41 KB.

### First & Last Rows

-   Displays the head and tail of the DataFrame to provide a quick preview of the data.

### Statistical Summary

-   `df.describe()` provides descriptive statistics for numeric columns ('Year', 'Rating', 'Rank').
-   **Key Findings**:
    -   Average Rating: ~8.82
    -   Rating Range: 8.6 - 9.3
    -   `Year` column currently shows `NaN` for all values, indicating an issue during scraping or parsing for this specific field. **(Note: This needs to be addressed if Year analysis is crucial.)**

### Missing Values Analysis

-   The analysis reveals that the 'Year' column has 25 missing values (all entries), accounting for 25% of the total data points in the DataFrame.
-   Other columns ('Title', 'Rating', 'Rank') have no missing values.

### Data Quality Check

-   No duplicate rows were found.
-   All 25 titles are unique.
-   0 unique years (due to missing values).
-   8 unique rating values.

### Rating Distribution

-   Most movies have ratings between 8.5 and 9.0 (22 movies).
-   3 movies have ratings between 9.0 and 9.5.

### Distribution Hypothesis

-   **Skewness**: 0.8585 (Positive skew, indicating a longer tail on the right side, though visually the distribution is clustered).
-   **Kurtosis**: 0.0338 (Near zero, suggesting a mesokurtic distribution, similar to a normal distribution in terms of peak/tails).

### Anomaly Detection

-   Using the IQR method, no outliers were detected in the 'Rating' column.

### Correlation Analysis

-   **Key Findings**:
    -   A strong negative correlation (-0.946) exists between 'Rank' and 'Rating', which is expected as lower ranks correspond to higher ratings on IMDB's top-rated list.
    -   Correlation with 'Year' is `NaN` due to all missing values in the 'Year' column.

## 4. Visualizations

Several plots are generated to visually represent the data and relationships:

-   **Rating Distribution (Histogram)**: Shows the frequency of different rating scores, with a vertical line indicating the mean rating.
-   **Rating Boxplot**: Provides a visual summary of the rating distribution, including median, quartiles, and potential outliers (none found here).
-   **Rank vs Rating (Scatter Plot)**: Illustrates the inverse relationship between a movie's rank and its rating.
-   **Correlation Heatmap**: Visualizes the correlation matrix between 'Rank', 'Year', and 'Rating'.
-   **Top 10 Highest Rated Movies (Horizontal Bar Chart)**: Displays the titles and ratings of the top 10 movies based on their IMDB rating.

## Conclusion

This notebook successfully scrapes the IMDB Top 50 movies, preprocesses the data, and performs an initial EDA. The analysis highlights the strong inverse relationship between rank and rating, confirms the absence of rating outliers within the top 50, and identifies a significant issue with missing 'Year' data that would need further investigation or refinement of the scraping logic to enable time-based analysis.
```
