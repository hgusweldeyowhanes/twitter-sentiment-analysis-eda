# Twitter Sentiment Analysis and Exploratory Data Analysis (EDA)

This repository contains a complete workflow for analyzing a Twitter dataset with sentiment labels. 
The project includes data cleaning, visualization, and exploratory analysis to understand sentiment distribution across topics.


## Dataset

 **File:** `twitter_training.csv`
 **Columns:** 
  -> 'ID' — Unique tweet identifier  
  -> 'Topic' — Topic of the tweet  
  -> 'Sentiment' — Sentiment label (Positive, Negative, Neutral, Irrelevant)  
  -> 'Text' — Content of the tweet  

 **Dataset Size:** 74,682 entries (after removing missing values and duplicates: 71,656 entries)  


## Project Goals

1. **Data Cleaning**
   -> Handle missing values
   -> Remove duplicates

2. **Exploratory Data Analysis (EDA)**
   -> Visualize distribution of topics using bar plots
   -> Visualize sentiment distribution using count plots and pie charts
   -> Analyze top topics with positive, negative, neutral, and irrelevant sentiments
   -> Examine message lengths by sentiment
   -> Plot a heatmap of topic vs sentiment
   -> Generate word clouds for topics and tweet text

3. **Visualization**
   -> Histograms, boxplots, count plots, pie charts
   -> Heatmaps and word clouds

## Libraries Used

-> `pandas` and `numpy` for data manipulation  
-> `matplotlib` and `seaborn` for visualization  
-> `wordcloud` for generating word clouds  
-> `warnings` to suppress warnings during analysis  


## Example Workflow

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from wordcloud import WordCloud

# Load dataset
cols = ['ID','Topic','Sentiment','Text']
train = pd.read_csv('twitter_training.csv', names=cols)

# Data cleaning
train.dropna(inplace=True)
train.drop_duplicates(inplace=True)

# Visualization
plt.figure(figsize=(8,10))
train['Topic'].value_counts().plot(kind='barh', color='b')
plt.xlabel("Count")
plt.show()

# Sentiment distribution
sns.countplot(x='Sentiment', data=train, hue='Sentiment', palette='viridis')
plt.show()

# Word cloud of all tweet text
corpus = ' '.join(train['Text'])
wc = WordCloud(width=1200, height=500).generate(corpus)
plt.imshow(wc, interpolation='bilinear')
plt.axis('off')
plt.show()
