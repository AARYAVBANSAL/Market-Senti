Challenge 1: Efficient Storage

import pandas as pd
import sqlite3

df = pd.read_csv("stock_prices.csv")
df["Date"] = pd.to_datetime(df["Date"])

conn = sqlite3.connect("market_data.db")
df.to_sql("stock_prices", conn, if_exists="replace", index=False)
df.to_parquet("stock_prices.parquet")
conn.close()

Challenge 4: Timezone Alignment

import pandas as pd
from datetime import time

MARKET_CLOSE = time(15, 30)

def map_day(ts):
    ts = pd.to_datetime(ts)
    if ts.weekday() >= 5 or ts.time() > MARKET_CLOSE:
        return (ts + pd.tseries.offsets.BusinessDay(1)).date()
    return ts.date()


Challenge 2

import spacy

nlp = spacy.load("en_core_web_sm")

articles = [
    "Apple released its quarterly earnings beating expectations.",
    "Apple is a fruit rich in fiber and vitamins.",
    "Amazon plans to expand its cloud business in India.",
    "Deforestation in the Amazon is increasing rapidly.",
    "Amazon announced layoffs across multiple departments."
]

company_name = "Apple"

def ner_org_filter(text, company):
    doc = nlp(text)
    for ent in doc.ents:
        if ent.text.lower() == company.lower() and ent.label_ == "ORG":
            return True
    return False

filtered_articles = []

for article in articles:
    if ner_org_filter(article, company_name):
        filtered_articles.append(article)

filtered_articles






    

