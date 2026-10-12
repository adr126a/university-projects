# University Projects - Data Science (LUMSA University)

Projects from my BSc in Data Science at LUMSA University, Rome: NLP, big data with Spark, text mining in R and a small scraping script.

| Project | Topic | Language / Tools |
| --- | --- | --- |
| [Fake News Detection](fake-news-detection/fake_news_detection.ipynb) | Bachelor's thesis: classifying political statements as real or fake | Python, scikit-learn, NLTK |
| [E-commerce Sales Analysis](spark-ecommerce-analysis/spark_ecommerce_analysis.ipynb) | Big Data course: orders by day, hour and department | PySpark, Spark SQL, Databricks |
| [Twitter - Circular Economy](twitter-circular-economy/twitter_circular_economy.ipynb) | Text mining: frequent terms, sentiment, topics, hashtags | R (tm, quanteda, syuzhet, BTM) |
| [Link Extractor](link-extractor/find_links.py) | Script that lists the external links of a web page | Python, requests |

## Fake News Detection

Binary classification of statements from the [LIAR dataset](https://www.cs.ucsb.edu/~william/data/liar_dataset.zip) using only the statement text.

- Preprocessing: lowercase, letters only, stopword removal, Porter stemming
- Features: Bag of Words with 1-3 n-grams, top 5,000 terms
- Models: Multinomial and Gaussian Naive Bayes, AdaBoost, Decision Tree, Logistic Regression, Random Forest, SVM, Perceptron
- Best result: Random Forest, 65.0% accuracy on the test set (majority-class baseline: 57.4%)

**Known limitations** (kept as in the original thesis so the reported results stay reproducible):
- The vectorizer is fitted on the full corpus before the train/test split (mild leakage).
- Speaker and context metadata available in LIAR are not used.
- Gaussian Naive Bayes is not suited to sparse count features.
- A single train/test split is used instead of cross-validation.

## E-commerce Sales Analysis

PySpark notebook run on Databricks over an e-commerce dataset with `orders`, `products` and `departments` tables. It counts orders, finds the busiest days and hours, and ranks departments by number of products. An HTML export with all outputs is included. Printed answers are in Italian, as in the original assignment.

## Twitter - Circular Economy

R notebook analysing tweets about the circular economy: term frequencies, word associations, n-grams, sentiment (Syuzhet, NRC, Bing), biterm topic modelling and hashtag extraction.

## How to run

```bash
pip install -r requirements.txt
python -m nltk.downloader stopwords
```

- **Fake news**: place `liar.csv` in `fake-news-detection/` and run the notebook.
- **Spark**: import the notebook into Databricks and upload the three CSV files to the paths used in the first cell.
- **Twitter**: open the notebook with an R kernel, install the packages listed in the first code cell and place `CE.csv` in `twitter-circular-economy/`.
- **Link extractor**: `python link-extractor/find_links.py`

Datasets are not included in this repository.
