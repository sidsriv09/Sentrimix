# SENTRIMIX
**Veritas AI Hackathon – Challenge 4.2.4: News Headlines and the Stock Market**  
**Track: Finance**

## 1. The Problem

The aim of our project was to investigate whether current-affairs news headlines, including geopolitical events, international relations and corporate developments, could be used to identify patterns in stock-market movements.

News can influence investor confidence and market behaviour. However, understanding how different headlines relate to financial markets can be difficult, particularly when large amounts of information need to be analysed.

I wanted to explore whether artificial intelligence and machine learning could analyse the sentiment of news headlines and use this information to predict the direction of the Dow Jones Industrial Average (DJIA).

## 2. What We Built

I developed **SENTRIMIX**, a system that allows users to input multiple news headlines and analyse their potential relationship with stock-market movements.

Each headline is processed using FinBERT, a language model designed to analyse financial sentiment. It classifies the headline as positive, negative or neutral and provides a score representing the strength of each sentiment.

These results are exported into a CSV file, with one row for each headline. I then aggregate the sentiment scores by day and use them as features in a Logistic Regression model.

The model predicts the likely direction of the DJIA, providing probabilities for the predicted outcomes. My system aims to make it easier to understand how the overall sentiment of news headlines may relate to market movements.

## 3. How It Works

### Dataset

I used the Kaggle dataset *Daily News for Stock Market Prediction*, created by J. Sun (2016). It contains historical news headlines alongside stock-market information, allowing us to investigate the relationship between news sentiment and market movements.

### Sentiment Analysis Using FinBERT

I selected FinBERT, developed by ProsusAI, because it is specifically designed for financial language. General sentiment analysis models may struggle to understand financial terminology, where words can have different meanings depending on their context.

FinBERT classifies each headline as positive, negative or neutral. These classifications are converted into numerical sentiment scores, which can then be used as inputs for our predictive model. I observed thie output of this analysis as a CSV file, which can be seen in the repository and the PowerPoint.

### Aggregating the Data

After analysing the individual headlines, I exported the results into a CSV file. I then combine the sentiment information by day to create a daily representation of the overall news sentiment.

This allows the predictive model to consider the general sentiment of the day's headlines rather than treating every headline as an entirely separate market event. The result of this can also be seen in the repository and the PowerPoint.

### Choosing Logistic Regression

I chose Logistic Regression because our objective was to predict the direction of the stock market, making this a classification problem.

Logistic Regression estimates the probability of an outcome belonging to a particular class. This was useful for my project because we wanted to provide probabilities alongside predictions, rather than simply producing an answer without indicating the model's level of certainty.

Another advantage is that Logistic Regression is relatively straightforward to interpret. It allowed me to investigate how changes in our sentiment features relate to the probability of an upward or downward market movement.

I also considered alternative algorithms, including Random Forest. However, my investigation suggested that the relationship between our selected features and the target variable was relatively linear. Random Forest did not provide a clear advantage for the patterns we observed, so Logistic Regression was a more suitable choice for our initial implementation.

I therefore prioritised using a model that was appropriate for the relationships in our data rather than introducing unnecessary complexity.

## 4. Results and Limitations

My model achieved a maximum reported accuracy of approximately **62%**.

I compared this against two simple baselines:
- Always predicting that the market would go up, which achieved approximately 50% accuracy.
- Predicting that the market would move in the same direction as the previous day, which achieved approximately 45% accuracy.

These comparisons suggest that the sentiment features may contain useful information about market direction.

However, my model also has limitations. One of the main difficulties I encountered was analysing headlines containing both positive and negative information, or headlines where the meaning was more complex than the wording initially suggested.

For example, a headline describing a slight increase in shipping costs could be classified as positive because of the word "increase", even though higher shipping costs could have negative implications for businesses and the wider economy.

This highlights an important limitation of sentiment analysis: linguistic sentiment does not always reflect the actual economic impact of an event.

Financial markets are also influenced by many factors beyond news headlines, including interest rates, inflation, company performance and wider economic conditions. Therefore, news sentiment alone cannot fully explain stock-market movements.

## 5. What I Would Improve With More Time

Although SENTRIMIX produced promising initial results, there are several areas I would investigate further to improve its accuracy and reliability.

### 5.1 Compare Different Sentiment Analysis Models

I would investigate alternative sentiment analysis models to determine whether FinBERT is the most suitable option for our project.

For example, I could compare it with other transformer-based models, such as RoBERTa, or sentiment analysis services offered by providers such as Microsoft Azure and Google Cloud.

I would test the models using the same set of manually labelled headlines and compare their accuracy, precision, recall and F1 scores.

This would help me establish whether another model could better understand financial terminology, complex headlines and the differences between linguistic sentiment and actual economic impact.

### 5.2 Introduce More Features Through Feature Engineering

We would explore adding more features to our dataset to give the predictive model a broader understanding of the factors that could influence market movements.

For example, I could introduce separate indicators for different types of news, such as:
- Geopolitical conflicts and international relations.
- Trade restrictions and tariffs.
- Energy prices and supply-chain disruptions.
- Corporate announcements and financial performance.

I could also investigate additional sentiment-based features, such as the number of positive, negative and neutral headlines per day, changes in overall sentiment and daily sentiment volatility.

In addition, incorporating historical market information, such as previous DJIA movements, trading volume and daily returns, could help the model identify patterns that are not explained by news sentiment alone.

### 5.3 Investigate Overfitting, Variance and Regularisation

With more time, I would investigate whether our model was overfitting the training data and whether its predictions would remain reliable when applied to unseen data.

Overfitting occurs when a model learns patterns that are specific to its training data rather than identifying relationships that can be applied to new information. This can result in strong performance during training but weaker performance when making predictions on unseen data.

I would use separate training, validation and test datasets, arranged chronologically because stock-market data is time-dependent.

- **Training data** would be used to teach the model and identify patterns.
- **Validation data** would be used to compare model settings and identify potential overfitting.
- **Test data** would be kept separate until the final evaluation to provide a more independent measure of performance.

I would also investigate regularisation, which is a technique used to reduce overfitting in Logistic Regression.

Regularisation works by applying a penalty to overly large model coefficients. This discourages the model from relying too heavily on individual features and helps control its complexity.

The strength of this penalty can be adjusted. If regularisation is too weak, the model may overfit the training data. If it is too strong, the model may become too simple and fail to identify useful patterns.

I would experiment with different regularisation strengths using the validation data to find a suitable balance. I would then evaluate the final model using the separate test dataset.

This could help us determine whether the model is learning meaningful relationships between news sentiment and market movements, rather than simply memorising patterns in historical data.

### 5.4 Improve the Interpretation of Geopolitical and Financial Sentiment

I would further investigate how different categories of news influence the sentiment features used by our predictive model.

For example, geopolitical disagreements, international trade restrictions and energy supply concerns may have different implications for financial markets, even if FinBERT assigns them similar negative sentiment scores.

I would investigate whether introducing separate indicators for these categories could help the model distinguish between different types of negative news.

This would allow me to explore whether certain geopolitical developments have a stronger relationship with DJIA movements than others.

I would also investigate whether combining multiple headlines into a daily sentiment indicator provides a more representative picture of market sentiment than analysing individual headlines independently.

## 6. Conclusion

SENTRIMIX demonstrates how natural language processing and machine learning can be combined to explore the relationship between news headlines and stock-market movements.

By using FinBERT to analyse financial sentiment and Logistic Regression to predict market direction, I developed a system that turns large amounts of textual information into numerical features that can be used for financial prediction.

Our initial results were promising, achieving a maximum reported accuracy of approximately 62%. However, I recognise that financial markets are influenced by many interconnected factors and that sentiment analysis has limitations when interpreting complex or mixed headlines.

With more time, I would focus on improving sentiment classification, introducing additional features and investigating the reliability of our model through further testing and regularisation.

Overall, SENTRIMIX demonstrates the potential of AI to identify relationships between current affairs and financial markets, while highlighting the challenges involved in making reliable predictions in a complex and constantly changing environment. Through analysis of corporate/business and geopolitical headlines, it appeared that corporate/business headlines had a more significant model prediction.

## 7. Further Materials (Please Read - provides useful background)
Geopolitics: https://drive.google.com/file/d/1GbHoaWfc4MxudXzqsQsR1YjXvODgaK9f/view?usp=sharing

Corporate/Business: https://drive.google.com/file/d/1zFd2_rcoLWnbobtnftzZA3on4d_ZJLg9/view?usp=drive_link

Video Demonstration: https://drive.google.com/file/d/1B4Yo5unLQX1mx_KzAAaWQ-DlVJnZWIME/view?usp=sharing

The PowerPoint is included in submission - please read, it gives a good summary of the project's development.

## 8. Sources

- Sun, J. (2016). *Daily News for Stock Market Prediction*. Kaggle: https://www.kaggle.com/datasets/aaron7sun/stocknews
- ProsusAI. *FinBERT*: https://huggingface.co/ProsusAI/finbert
