<h1 align="center">Entity-Level Sentiment Analysis of YouTube Comments</h1>
<h3 align="center">Unlocking Audience Sentiment</h3>

<p align="center">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/578d03ab-8d2a-42ad-af19-5eac0237a06f" width="300">
</p>

YouTube is a massive platform where people engage with content and each other. Comments play a big role in this interaction, showing different opinions and feelings. But understanding how people feel about specific things like videos or creators is tough. It's crucial to know this sentiment to see how viewers are reacting and improve content strategies. This project uses advanced NLP methods to analyze YouTube comments and figure out how people feel about different parts of the platform

## Data Exprolation

**Training set shape**: (74681, 4)  
**Validation set shape**: (999, 4)

<p align="left">
<img src = "https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/f580dd2d-d65d-43d9-b6a3-59453856cc96" width = 800>
</p>

Initially, the data lacked headers. Therefore, we added column names to enhance comprehension of the dataset:

<p align="left">
<img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/77f1296a-8e9c-4731-bba3-65bb5bee1548" width = 800>
</p>

- **video_id**: A distinct marker for every comment tweet.
- **entity**: The focal point of interest linked with the comment (e.g., video ID, creator name).
- **sentiment**: The emotional categorization assigned to the comment concerning the specified entity. There are three categories: Positive, Negative, Neutral. Messages unrelated to the entity are classified as Neutral.
- **comment**: The written content of the video remark.

<p align="left">
<img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/df55f15a-0e6e-402c-b119-a93b5564e934" width = 800>
</p>

- Created a new column named 'comment_word_count' to calculate the word count in each comment. Observed that the average word count per comment ranges from 5 to 30.

<p align="left">
<img src= "https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/24bca03b-abbf-45cb-b1d8-71a883568156" width = 800>
</p>

- Identified extreme outliers in our data by implementing a condition where the word count exceeds 125. This approach enables us to examine comments with exceptionally high word counts along with their corresponding sentiments. from this analysis, we can understand if there's anything unusual or strange in our data.

## Data Preprocessing


<p align="left">
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


<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/3c27fd8a-18b3-49da-9c9b-96fea96b9821" width=800>
</p>

Now, for sentiment analysis of those extracted entities, we utilized both TextBlob and VADER methods.
- For a simple and easy-to-implement solution for basic sentiment analysis, TextBlob might suffice. 
- However, for analyzing social media text with informal language and emoticons, and for more detailed sentiment analysis, VADER could be a better choice. It's often beneficial to experiment with both methods and evaluate their performance based on the use case. 

After trying both, we found VADER to be the most suitable for our analysis.


<p align="left">
  <img src = "https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/345f026c-c6f9-4aae-9d27-5950cc191628" width=400>
</p>
<p align="left">
  <img src = "https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/adf8b118-14c6-44df-bcfa-9d18737d4568" width=400>
</p>

## Visualizing Sentiments of Comments

To identify the primary words used per label, a word cloud was generated to visualize the most significant words within the training data.

1. Positive Sentiment

<p align="left">
  <img src = "https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/01a34ff3-95dc-4da9-a24c-a287008f3a04" width=600>
</p>

In comments labeled as positive, words like love, game, thank, good, best, amazing and great were commonly used, alongside a diverse range of words conveying positive sentiments.

2. Negative Sentiment

In contrast, negative comments predominantly featured curse words, along with mentions of specific games and industries such as Twitter, Facebook, and dead redemption.

<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/87fd5807-aee9-4b04-b3d0-d73c6cba4a19" width="600">
</p>

3. Neutral Sentiment

Neutral comments, on the other hand, have few curse words, same words as before and differed significantly in terms of important words compared to the other sentiment categories like Italy, twitch tv etc.

<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/5d813002-ddcf-447c-9f00-e5afad484888" width="600">
</p>

**Distribution of Comments per Topic and Sentiment**

<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/40b1edc3-66df-4e7d-ac04-6965658b36f7" width=800>
</p>

Above barplot shows that for games such as ReadDeadRedemption(RDR) and Battelfield has the number of negative comments is the highest while on the other brands the trend is different. Amazon has highest positive comments.

**Distribution of Sentiments**

<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/5deb9af0-5148-4952-b017-ee2ac18de67f" width="300">
</p>

- Sentiment 'Negative’: 47.4%
  - Minimum Commment Count '518' at Entity 'AssassinsCreed'
  - Maximum Comment Count '1326' at Entity 'RedDeadRedemption(RDR)’

- Sentiment 'Positive’: 36%
  - Minimum Commment Count '565' at Entity 'RedDeadRedemption(RDR)'
  - Maximum Comment Count '1519' at Entity 'Amazon'

- Sentiment 'Neutral’: 16.6%
  - Minimum Commment Count '183' at Entity 'Amazon'
  - Maximum Comment Count '508' at Entity 'PlayStation5(PS5)'

### Insights 

Performed Positive/Negative sentiment distribution by Entities.
- The data indicates that Amazon comments exhibit the most positive sentiment (67.09%) among the discussed entities, with subsequent positive sentiments found in comments related to AssassinsCreed, Hearthstone, and Borderlands.
- Conversely, RedDeadRedemption (RDR) comments display the highest level of negative sentiment (61.33%) in our dataset.

Additionally, retrieved the Top Positive/Negative Entities from comments.
- The majority of positive comments regarding Amazon are related to Manga, with people sharing comments about the volumes of Kamuy and Hakusho sold on the platform. However, there are a few comments mentioning Jeff Bezos and Amazon that express negative sentiment.
- In contrast, comments about the game Red Dead Redemption mostly convey negative sentiments. Entities like Arthur Morgan and Tsushima are the top negative sentiment entities. It's possible that people are comparing the game and its protagonist, Arthur Morgan, with another game called "Ghost of Tsushima."
- Regarding Assassins Creed, positively sentimented entities include Netflix and Demon Souls. People are enthusiastic and post positive comments about a brand-new, live-action Assassin's Creed series coming to Netflix. Additionally, they relate Demon Souls video game with Assassins Creed in a positive light.


## Feature Extraction

**Bag of words (BoW)** is a traditional text representation technique that is widely used in NLP, particularly in text classification problems. The main idea is to represent the text under consideration as a bag (collection) of words, ignoring the order and context.

<p align="center">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/ca1acfc9-c72c-48f1-9429-0e1fc2e8f6a8" width=500>
</p>

**Term frequency-inverse document frequency**, or **TF-IDF**, method attempts to quantify the importance of a given word in relation to other words in the document and in the corpus.

<p align="center">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/bf76cd76-6de7-4961-b651-8c94e601e0d5" width=500>
</p>

**Difference between BOW and TF IDF**

- CountVectorizer simply counts the number of times a word appears in a document (using a bag-of-words approach).
- While TF-IDF Vectorizer takes into account not only how many times a word appears in a document but also how important that word is to the whole corpus.

After performing CountVectorizer() and TfidfVectorizer(), X_train_bow, X_val_bow, X_train_tfidf, and X_val_tfidf contain the feature representations of the comments using bag-of-words and TF-IDF techniques respectively.

## Model Development

**Bag-of-Words (BoW) based model with Logistic Regression**

<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/858471f0-f7cc-49ea-b928-207d532a4ca4" width=800>
</p>


**TF-IDF based model with SVM**

<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/58ca8299-4b62-4b0d-b3a5-6cdc626413f4" width=800>
</p>


## Model Training

<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/431f1913-fdb6-4866-9ece-feba7b2be279" width=800>
</p>


## Model Evaluation

<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/942d6e3f-12b2-4632-b4a5-9a7d5314160b" width=500>
</p>

<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/8fbd952c-e392-490b-aaf4-07f22b8e099e" width=500>
</p>

Also, displayed some actual vs predicted labels along with comment text

Based on the this, both the Logistic Regression model with Bag-of-Words (BoW) and the Support Vector Machine (SVM) model with TF-IDF achieve high accuracy on the validation dataset. Here's a summary of their performance:

- Logistic Regression (BoW) Validation Accuracy: 92.69%
- SVM (TF-IDF) Validation Accuracy: 92.55%

Both models also exhibit similar precision, recall, and F1-score across different sentiment classes.

Since the accuracy scores are very close, Logistic Regression with BoW tends to be more interpretable and computationally efficient compared to SVM with TF-IDF, especially for large datasets.

## Let’s Predict Random Live Comment 	

### @RedDeadRedemption(RDR)	
<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/193ba967-9dae-4077-9c19-bf29e9c55374" width=300>
</p>

<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/633a13ce-e7e3-472b-a252-97c04587f352" width=800>
</p>


### @GrandTheftAuto(GTA)	
<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/9b94ac38-c6a7-4787-baa2-3919527f1f35" width=800>
</p>

<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/cfa3515c-608e-46f7-a856-3af0ef424d31" width=800>
</p>


### @Battlefield
<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/061b2f58-e492-4b60-8af3-449494d6304d" width=500>
</p>

<p align="left">
  <img src="https://github.com/gentallman/Entity_Level_Sentiment_Analysis_of_YouTube_Comments/assets/78334851/07fc8e98-2158-4ae0-ac6c-2d8dbf9dbb26" width=800>
</p>

## Analysis and Interpretation

**Distribution of Sentiment Classes**

Thoroughly examined the distribution of sentiment classes (positive, negative, neutral) across the entities analyzed. We identified which entities have a predominant sentiment (positive, negative, or neutral) and which ones exhibit a more balanced sentiment distribution.

For example, Amazon exhibited the highest positive sentiment, while RedDeadRedemption (RDR) displayed the highest negative sentiment. This indicates that sentiment towards entities on YouTube comments is not uniform and can be influenced by factors such as brand reputation, product quality, and user experiences.

**Patterns and Trends**
- Positive Comments: Words like "love," "game," "thank," "good," "best," "amazing," and "great" were commonly used in positive comments. This suggests that users express satisfaction, appreciation, and enthusiasm towards certain entities.

- Negative Comments: Negative comments often featured curse words and mentions of specific games and industries such as Twitter, Facebook, and Red Dead Redemption. This indicates dissatisfaction, frustration, or criticism towards certain entities or their associated topics.

- Neutral Comments: Neutral comments had fewer curse words and differed significantly in terms of important words compared to positive and negative comments. This suggests a more balanced or indifferent stance towards the discussed entities.


** Challenges Encountered**

- Identification of Entities: One challenge encountered was accurately identifying entities mentioned in the comments. Entities may be referenced using various terms or aliases, requiring comprehensive entity recognition techniques.

- Handling Bias and Subjectivity: Another challenge was handling bias and subjectivity in sentiment analysis. Certain words or phrases may carry different sentiments depending on context, cultural factors, or user intent, necessitating careful consideration** and validation of sentiment labels.

## Contact

Author: [@Smit Rana](https://www.linkedin.com/in/smit98rana/)
<p align="center">
	<img src="https://user-images.githubusercontent.com/74038190/214644145-264f4759-7633-441e-9d67-d8dda9d50d26.gif" width="200">
</p>

<div align="center">
  <a href="https://git.io/typing-svg">
    <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&pause=1000&center=true&vCenter=true&random=true&width=435&lines=I+hope+this+work+serves+you+well!" alt="Typing SVG" />
  </a>
</div>

<img src="https://user-images.githubusercontent.com/74038190/212284100-561aa473-3905-4a80-b561-0d28506553ee.gif" >


