# Kenya News Scraper

Create a web scraper that aggregates news articles from multiple Kenyan media sources, extracts key information, analyzes sentiment, and presents the data in a simple dashboard like the one shown above.

- Citizen Digital
- Daily Nation
- The Standard Media
- The Star
- Tuko

Each scraper follows a standardized approach to extract article content, metadata, and categorize news items for analysis or archiving.

## Project Structure

```
Kenya_news1/
│
├── config/                  
│   ├── database.py          
│   └── settings.py          
│
├── scrapers/                
│   ├── base_scraper.py      
│   ├── citizen.py           
│   ├── daily_nations.py     
│   ├── standardmedia.py     
│   ├── star.py              
│   └── tuko_new.py          
│
├── utils/                   
│   ├── date_parser.py       
│   ├── logger.py            
│   └── text_cleaner.py      
│
├── logs/                    
├── main.py                  
└── setup.py
│           
│
├── modelling/                   
│   ├── kenya_new.ipynb      
│                      
│
├── Tableau/                   
│   ├── kenyanews1.xlsx       
│   ├── presentation.twb           
│   └── sentiment_count.csv
                
```

## Installation

### Prerequisites

- Python 3.12 or higher
- Firefox browser (for WebDriver)
- MySQL database (optional, for storage)

### Setup

1. Clone the repository:
   ```
   https://github.com/Denismwangi01/scraping-Kenyan-media-websites-and-performing-sentiment-analysis.git
   cd scraping-Kenyan-media-websites-and-performing-sentiment-analysis
   ```

2. Create a virtual environment:
   ```
   python -m venv venv
   source venv/bin/activate  
   ```

3. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

4. Configure database settings in `config/settings.py`

## Usage

### Running All Scrapers

To run all news scrapers:

```
python main.py
```

### Running Specific Scrapers

To run only specific scrapers:

```
python main.py --sources citizen star
```

Available sources: `citizen`, `daily_nations`, `standardmedia`, `star`, `tuko`

## Scraper Design

Each scraper extends the `BaseScraper` class, which provides common functionality:

- WebDriver initialization
- Database connection management
- Article existence checking
- Content saving
- Logging

The scrapers are designed to:
- Scrape up to 30 articles total by default (configurable)
- Distribute articles evenly across categories
- Extract article details including title, author, date, content, and category
- Use fallback mechanisms for content extraction when primary methods fail
- Handle relative URLs and website-specific page structures

Create Sentiment Analysis Module

- Implement sentiment analysis using a library like NLTK, TextBlob, or spaCy
  Calculate polarity scores (positive/negative/neutral) for each article
  Extract key words and their frequency for word cloud generation

## Features

- **Robust Content Extraction**: Multiple extraction methods with fallbacks
- **Smart Article Limits**: Configurable article limits to prevent overloading
- **Database Integration**: Stores articles in MySQL for easy querying
- **Duplicate Prevention**: Avoids re-scraping existing articles
- **Comprehensive Logging**: Detailed logs for debugging and monitoring
- **Error Handling**: Graceful error handling throughout the scraping process
- **Sentiment Analysis**: NLTK or TextBlob for sentiment scoring
- **Dashboard: Tableau** (as shown in the image) 



![image](https://github.com/user-attachments/assets/69ce5672-0c86-41ca-a262-dc2b90cf92c7)
This dashboard shows data bout sentiment analysis for Kenyan media websites. Some key points I notice:

Total count is 119 articles being analyzed. The sentiment breakdown shows 42.02% positive sentiments and only 9.24% negative sentements. The rest are possibly  neutral articles.


The graph in middle shows sentiments changing over time from January 2023 to April 2025. There was a big spike in positive sentiment around April 2023, then it dropped and slowly increased again over time.

The pie chart shows overall distribution of sentiments with blue for negative, orange for neutral, and red for positive. Looks like neutral content is biggest piece.

The word cloud shows common words in articles. Words like "tuko", "kenya", "read", "editor" appear alot. This shows what topics are popular in these media sites.

The top 4 articles section shows some articles by Jiji Ndogo with high polarity scores. The media house chart shows several outlets including Tuko Editors, Standard Group, KBC, and Citizen Media.
My observation is that Kenyan media  seems to have more positive than negative news, with certain media houses standing out in the analysis. The sentiment has been slowly improving since mid-2023.



## Customization

### Adjusting Article Limits

Each scraper has a `max_articles` property in the `__init__` method that can be modified to change the total article limit.

### Adding New Sources

To add a new news source:

1. Create a new scraper file extending `BaseScraper`
2. Implement the required methods: `scrape_article_page`, `scrape_category`, and `scrape`
3. Add the scraper to the `scrapers` dictionary in `main.py`

## Troubleshooting

- **WebDriver Issues**: Make sure Firefox is installed and geckodriver is in PATH
- **Database Errors**: Check connection settings in `config/settings.py`
- **Empty Content**: Some websites may change their structure; update selectors as needed
- **Rate Limiting**: Increase `wait_time` and `time.sleep()` intervals if getting blocked



## Acknowledgments

- BeautifulSoup4 for HTML parsing
- Selenium for browser automation
- Various Kenyan news sources for providing public content


## License

This project is licensed under the MIT License - see the LICENSE file for details. (http://www.apache.org/licenses/)
