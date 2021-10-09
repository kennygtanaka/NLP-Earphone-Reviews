# Natural Language Processing (NLP) on Earphone Reviews

Personal project analyzing text reviews for earphones on Amazon.

Libraries Used:
* NLTK (NLP)
* VADER (NLP)
* numPy (data)
* pandas (data)
* sklearn (model)
* seaborn (visualization)

This README file is the written overview of the project, all the code was written on a Jupyter Notebook which can be found in the repository.

# Data Used

Amazon Earphones Reviews - https://www.kaggle.com/shitalkat/amazonearphonesreviews

# Introduction

The data is comprised of reviews on 11 different earphones and has a total of 14,337 reviews.

This project aims to achieve two main goals:
1. Understand which earphones received positive and negative reviews through EDA and sentiment analysis.
2. Create a model that predicts star ratings using VADER compound sentiment values and other variables as input.

# EDA (Exploratory Data Analysis)

First, the count of star reviews for each star rating was analyzed.

![alt text](/images/image_1.png?raw=true)

The bar chart showed that there were significantly more five star reviews and less two and three star reviews.

Next, the length of reviews was observed against the number of stars given.

![alt text](/images/image_2.png?raw=true)

Two and three star reviews were longer on average and five star reviews were shorter, presumably because the customer was satisfied. What was surprising is that the one star reviews were shorter than the two and three star reviews.

From there the rating trends of the products themselves were studied.

![alt text](/images/image_3.png?raw=true)

The Flybot and Sennheiser earphones seem to have the highest reviews, however the FLybot Boom seems to have a high deviation in ratings. The JBL earphones were rated the lowest with Skullcandy a close second worst.

Lastly, the earphones were compared utilizing a heatmap to see if there were any patterns in stars and text length for specific earphones.

![alt text](/images/image_4.png?raw=true)

It can be seen here that the Flybot Boom had a large amount of three star ratings. Since it had the highest rating in the previous bar chart shown, customers seem to either really enjoy the Flybot Boom or find it mediocre.

# Sentiment Analysis

After the exploratory data analysis, sentiment analysis of the reviews (title and body) was run using the NLTK and Vader libraries. Negative, neutral and positive ratings were given to each review depending on the sentiment of all the words. The VADER library also outputs a compound sentiment value which is the combined total of the negative, neutral and positive ratings of the words in each review. A value between -1 (negative sentiment) and 1 (positive sentiment) was given to each of the reviews.

The following visualization shows the average negative, neutral and positive scores for each star rating:
![alt text](/images/image_5.png?raw=true)

As expected, five star ratings have the highest average score of positive text sentiment and one star ratings have the highest negative rating. According to the sentiment data, it seems that positive reviews are much happier about their products than negative reviewers are angry/sad about their products. One unexpected observation with the neutral ratings is that there was a higher average for one star ratings than four star ratings. This may be due to the fact that a larger fraction of words were used for positive remarks.

# Positive or Negative Classification

Each of the VADER compound values were labelled as either negative or positive depending on if they were above or below the value of zero. The original one to five star ratings were also put into positive (four and five star) or negative (one to three star) categories. They were then compared and an accuracy of 0.83 or 83% was achieved. This means that the text from the reviews can predict whether a product had a negative or positive review correctly 83% of the time. This was the classification report that also portrays the other classification metrics:

![alt text](/images/image_6.PNG?raw=true)

# Prediction of Star Rating using Random Forest Classifier

For the final part of the project, a Random Forest Classifier was used to predict star ratings of earphone reviews. A classifier was used instead of a regressor since they generally tend to perform better on a low number of categories.

To get started, the earphone names were turned to hash identification numbers to be accepted as input for the classifier. This dictionary shows the earphones and their assigned hash numbers:

![alt text](/images/image_7.PNG?raw=true)

With all the training variables in numeric form, the data was ready to perform classification. The hash number for the product, sentiment values (negative, neutral, positive, compound) and text length. All the sentiment values were added since there isn't a major concern of multicollinearity with a Random Forest Classifier. The initial model with no hyperparameter optimization had an accuracy score of 0.51. The model's were then tuned with multiple iterations of cross validation hyperparameter optimization. Best parameters for the model are shown below:

![alt text](/images/image_8.PNG?raw=true)

The final model had an accuracy of 0.55. Star ratings of earphones can be predicted correctly from text sentiment about 55% of the time. Considering that there are five different star ratings this accuracy is not the worst.

# Moving Forward

To improve the accuracy of this model some of the things that can be done are:

* A wider variety of products and users can be collected data on.
* Utilizing different and more advanced NLP libraries other than VADER.
* The incorporation of a larger number of predictor variables.
* Experimenting with various forms of data transformations.
