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

![image](https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/f580dd2d-d65d-43d9-b6a3-59453856cc96)

Initially, the data lacked headers. Therefore, we added column names to enhance comprehension of the dataset:

![image](https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/77f1296a-8e9c-4731-bba3-65bb5bee1548)

- **video_id**: A distinct marker for every comment tweet.
- **entity**: The focal point of interest linked with the comment (e.g., video ID, creator name).
- **sentiment**: The emotional categorization assigned to the comment concerning the specified entity. There are three categories: Positive, Negative, Neutral. Messages unrelated to the entity are classified as Neutral.
- **comment**: The written content of the video remark.

![image](https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/82fe59df-617d-475c-af79-951c57b2f8a2)

![image](https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/39c5ea84-9e56-4b08-ae73-941586763b5c)

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

![image](https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/3c27fd8a-18b3-49da-9c9b-96fea96b9821)


