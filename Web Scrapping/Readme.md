
# IMDb Top 20 Movies Web Scraper 

## Overview

The goal of this notebook is to programmatically retrieve structured data (Top 20 Movies) from a dynamic web page (IMDb) using Python. It covers essential web scraping techniques and data manipulation with pandas.

## Libraries Used

 **`requests`**:
  
   A fundamental HTTP library for Python, used to send HTTP requests to web servers and retrieve their responses.

 **`BeautifulSoup` (from `bs4`)**:

A powerful library for parsing HTML and XML documents. It creates a parse tree from page source code that can be used to extract data from HTML in a highly flexible way.

 **`pandas`**:

 A fast, powerful, flexible, and easy-to-use open-source data analysis and manipulation tool, built on top of the Python programming language. It is used here to organize the scraped data into a DataFrame and export it.

## Notebook Workflow

The notebook executes the following steps:

1.  **Import necessary libraries**: Imports `requests`, `BeautifulSoup`, and `pandas` for web scraping and data handling.

2.  **Define URL and headers**: Specifies the target URL (`https://www.imdb.com/chart/top/`) and sets `User-Agent` headers to simulate a web browser, which helps in avoiding bot detection by the server.
   

3.  **Fetch HTML content**:

Uses `requests.get()` to fetch the HTML content of the IMDb page. The content is then parsed by `BeautifulSoup` into a navigable tree structure.
   
4.  **Identify movie elements**:

     Locates all `<li>` HTML elements with the class `ipc-metadata-list-summary-item`, which correspond to individual movie entries on the Top 250 list.
    
5.  **Initialize data storage**:
   
    Creates an empty dictionary (`movie_data`) with keys for 'Title', 'Year', 'Rating', and 'Rank' to store the extracted data.
   
6.  **Extract movie details**: Iterates through the first 20 identified movie elements:
   
    *   Extracts the movie title by parsing the text of the `h3` tag and cleaning up the ranking number.
      
    *   Extracts the release year from the first `span` tag with a specific class.
      
    *   Extracts the IMDb rating from another `span` tag associated with ratings.
  
    *   Determines the rank based on the iteration index.
      
    *   Appends the extracted information to the respective lists in the `movie_data` dictionary.
    
7.  **Create and display DataFrame**:

    Converts the `movie_data` dictionary into a pandas DataFrame.
    
8.  **Save to CSV**:

      Exports the DataFrame to a CSV file named `scraped_movies.csv` without including the DataFrame index. The DataFrame is also printed to the console for immediate review.

## Output

The execution of this notebook will produce:

-   A pandas DataFrame displayed in the notebook output, showing the top 20 movies with their titles, years, ratings, and ranks.
-   A CSV file named `scraped_movies.csv` containing the same structured data, saved in the Colab environment
    
**Python Code Link:**
https://github.com/Abbas786-Ali/Web-Scraping-project/tree/main/Web%20Scrapping
