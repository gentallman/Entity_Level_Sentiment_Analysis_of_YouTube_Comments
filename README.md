<h1 align="center">Entity-Level Sentiment Analysis of YouTube Comments</h1>
<h3 align="center">Unlocking Audience Sentiment</h3>

<p align="center">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/578d03ab-8d2a-42ad-af19-5eac0237a06f" width="300">
</p>

YouTube is a massive platform where people engage with content and each other. Comments play a big role in this interaction, showing different opinions and feelings. But understanding how people feel about specific things like videos or creators is tough. It's crucial to know this sentiment to see how viewers are reacting and improve content strategies. This project uses advanced NLP methods to analyze YouTube comments and figure out how people feel about different parts of the platform

## PROJECT OBJECTIVES

- **Data Exploration**
- **Data Preprocessing**
- **Visualizing Sentiments of Comments**
- **Feature Extraction**
- **Model Development**
- **Model Training**
- **Model Evaluation**
- **Predicting Sentiments**
- **Analysis and Interpretation**

## Data Exprolation

**Training set shape**: (74681, 4)  
**Validation set shape**: (999, 4)

<p align="center">
<img src = "https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/f580dd2d-d65d-43d9-b6a3-59453856cc96" width = 800>
</p>

Initially, the data lacked headers. Therefore, we added column names to enhance comprehension of the dataset:

<p align="center">
<img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/77f1296a-8e9c-4731-bba3-65bb5bee1548" width = 800>
</p>

- **video_id**: A distinct marker for every comment tweet.
- **entity**: The focal point of interest linked with the comment (e.g., video ID, creator name).
- **sentiment**: The emotional categorization assigned to the comment concerning the specified entity. There are three categories: Positive, Negative, Neutral. Messages unrelated to the entity are classified as Neutral.
- **comment**: The written content of the video remark.

<p align="center">
<img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/df55f15a-0e6e-402c-b119-a93b5564e934" width = 800>
</p>

- Created a new column named 'comment_word_count' to calculate the word count in each comment. Observed that the average word count per comment ranges from 5 to 30.

<p align="center">
<img src= "https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/24bca03b-abbf-45cb-b1d8-71a883568156" width = 800>
</p>

- Identified extreme outliers in our data by implementing a condition where the word count exceeds 125. This approach enables us to examine comments with exceptionally high word counts along with their corresponding sentiments. from this analysis, we can understand if there's anything unusual or strange in our data.

## Data Preprocessing


<p align="center">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/82fe59df-617d-475c-af79-951c57b2f8a2" width = 800>
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/39c5ea84-9e56-4b08-ae73-941586763b5c" width = 800>
</p>
- Created a dictionary that includes all emojis along with their meanings. Additionally, made a dictionary of contractions to prepare the YouTube comments for use in further NLP models.

### Comment Text Processing

Created a preprocessing function with the following tasks by defining regular expressions:

- **Lowercasing**: Converts all text to lowercase to ensure consistency.
  ```python
  lower()
  ```
- **URL Replacement**: Replaces all URLs in the text with the word 'URL’.
  ```python
  r"((http://)[^ ]*|(https://)[^ ]*|( www\.)[^ ]*)"
  ```
- **Emoji Replacement**: Replaces emojis with their meanings (e.g., 😊 becomes EMOJIsmiling_face).
- **Special Character Removal**: Removes special characters and non-alphanumeric characters.
  ```python
  "[^a-zA-Z0-9]"
  ```
- **Sequence Reduction**: Reduces sequences of three or more consecutive letters to just two letters (e.g., 'hellooooo' becomes 'hello’).
  ```python
  r"(.)\1\1+"
  r"\1\1"
  ```
- **Contraction Expansion**: Expands contractions (e.g., "don't" becomes "do not").
- **Stopword Removal and Lemmatization**: Removes stopwords (words like 'and', 'the', 'is') and lemmatizes words (reduces them to their base form).


After preprocessing the data, performed Entity Extraction. This involved extracting entities such as persons, products, organizations, and geopolitical entities from YouTube comments to analyze the sentiment associated with each one.


<p align="center">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/3c27fd8a-18b3-49da-9c9b-96fea96b9821" width=800>
</p>

Now, for sentiment analysis of those extracted entities, we utilized both TextBlob and VADER methods.
- For a simple and easy-to-implement solution for basic sentiment analysis, TextBlob might suffice. 
- However, for analyzing social media text with informal language and emoticons, and for more detailed sentiment analysis, VADER could be a better choice. It's often beneficial to experiment with both methods and evaluate their performance based on the use case. 

After trying both, we found VADER to be the most suitable for our analysis.


<p align="center">
  <img src = "https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/345f026c-c6f9-4aae-9d27-5950cc191628" width=400>
</p>
<p align="center">
  <img src = "https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/adf8b118-14c6-44df-bcfa-9d18737d4568" width=400>
</p>

## Visualizing Sentiments of Comments

To identify the primary words used per label, a word cloud was generated to visualize the most significant words within the training data.

1. Positive Sentiment
<p align="center">
  <img src = "https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/01a34ff3-95dc-4da9-a24c-a287008f3a04" width=800>
</p>


