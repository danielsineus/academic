

---
title: 'NATURAL LANGUAGE PROCESS'
  
author: Daniel Sineus
date: '2023-10-12'
slug: NLP Data Science Projects
categories:
  - research
tags:
  - Natural Language
  - Regression Analysis
subtitle: ''
summary: ''
authors: []
lastmod: '2023-10-12T22:00:09-04:00'
featured: no
draft: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---


<h1 align="center">
    NLP Data Science Projects
</h1>
  
<h2 align="center">
    Project: Sentiment Analysis of Movie Reviews
</h2>

<h3 align="center">
 Daniel SINEUS
</h3>


### **NLP project**

**Context:** I have realized this project in the context of a training with National Student Data Corps (NSDC).
The National Student Data Corps (NSDC) is a community-developed initiative that provides resources and opportunities for students to learn data science, in a community of support, with a special focus on engaging underserved institutions, students, and communities. If you want to know more about this organization, please click on this link below:
https://nebigdatahub.org/nsdc/

**Project Description:**

This project will introduce students to an array of skills as they strive to create a sentiment analysis model to classify a given review as positive or negative. Sentiment Analysis leverages both Natural Language Processing and Machine Learning skills - how to represent text in a machine-understandable format so as to classify the text and extract sentiment. We will also cover visualizations and how to deploy models in the real world.


---
---



<h3 align = "center">
    Milestone #1
</h3>



GOAL: The main goal of this milestone is to set up your environment, install the required packages, learn how to acces data and do some basic exploratory data analysis.

**Step 1:**

Setting up libraries and installing packages

To install a library:
```python
 import <library> as <shortname>
```
We use a *short name* since it is easier to refer to the package to access functions and also to refer to subpackages within the library.



```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from nltk.tokenize import word_tokenize,sent_tokenize
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.preprocessing import LabelBinarizer
from sklearn.naive_bayes import MultinomialNB
from sklearn.metrics import accuracy_score

```

These are the libraries that will help us throughout this project. It is not necessary that you know what each library does, but you can always look it up.

We encourage you to read more about the important and most commonly used packages like Pandas and Natural Language Toolkit (NLTK) and write a few lines in your own words about what they do. [You may use the Data Science Resource Repository (DSRR) to find resources to get started!](https://nebigdatahub.org/nsdc/data-science-resource-repository/)



<h4 style="color:orange">
  
</h4>

It is important to know about some libraries such as Pandas and NLTK

- **Pandas:**

Pandas is a Python package that provides fast, flexible, and expressive data structures designed to make working with "relational" or "labeled" data both easy and intuitive. It aims to be the fundamental high-level building block for doing practical, real world data analysis in Python. Additionally, it has the broader goal of becoming the most powerful and flexible open source data analysis / manipulation tool available in any language.

**Main Features**

Here are just a few of the things that pandas does well:

Easy handling of missing data (represented as NaN, NA, or NaT) in floating point as well as non-floating point data
Size mutability: columns can be inserted and deleted from DataFrame and higher dimensional objects
Automatic and explicit data alignment: objects can be explicitly aligned to a set of labels, or the user can simply ignore the labels and let Series, DataFrame, etc. automatically align the data for you in computations
Powerful, flexible group by functionality to perform split-apply-combine operations on data sets, for both aggregating and transforming data
Make it easy to convert ragged, differently-indexed data in other Python and NumPy data structures into DataFrame objects
Intelligent label-based slicing, fancy indexing, and subsetting of large data sets
Intuitive merging and joining data sets
Flexible reshaping and pivoting of data sets
Hierarchical labeling of axes (possible to have multiple labels per tick)
Robust IO tools for loading data from flat files (CSV and delimited), Excel files, databases, and saving/loading data from the ultrafast HDF5 format
Time series-specific functionality: date range generation and frequency conversion, moving window statistics, date shifting and lagging


- **NLTK:**

NLTK is a leading platform for building Python programs to work with human language data. It provides easy-to-use interfaces to over 50 corpora and lexical resources such as WordNet, along with a suite of text processing libraries for classification, tokenization, stemming, tagging, parsing, and semantic reasoning, wrappers for industrial-strength NLP libraries, and an active discussion forum.

NLTK has been called “a wonderful tool for teaching, and working in, computational linguistics using Python,” and “an amazing library to play with natural language.”

Natural Language Processing with Python provides a practical introduction to programming for language processing. Written by the creators of NLTK, it guides the reader through the fundamentals of writing Python programs, working with corpora, categorizing text, analyzing linguistic structure, and more.

According to Joanna Jablonski (n.d), Natural language processing (NLP) is a field that focuses on making natural human language usable by computer programs. NLTK, or Natural Language Toolkit, is a Python package that you can use for NLP.

**References**

Jablonski, J. (n.d.). Natural Language Procesing with Python's NLTK Package. Real Python. https://realpython.com/nltk-nlp-python/


Pandas Development Team (2008-2011). PANDAS: Powerful Python Data Analysis Toolkit. Pandas 2.01.1.  https://pypi.org/project/pandas/

NLTK Team (2023). Documentation: Natural Language Toolkit. NLTK. https://www.nltk.org/

---

**Step 2:**

Let’s access our data. We will be using the Internet Movie Database (IMDb) as our dataset. The dataset contains 50,000 movie reviews from the Internet Movie Database. Reviews have been pre-labeled with sentiment polarity (positive/negative).  


[The IMDb Movie Reviews dataset is available at this link](https://raw.githubusercontent.com/meghjoshii/NSDC_DataScienceProjects_SentimentAnalysis/main/IMDB%20Dataset.csv). It is better to use the link provided directly within the read_csv function.



We will use pandas to read the data from the csv file using the `read_csv` function. This function returns a pandas dataframe. We will store this dataframe in a variable called `df`.


```python
#Read the data using pandas read_csv function
df=pd.read_csv("https://raw.githubusercontent.com/meghjoshii/NSDC_DataScienceProjects_SentimentAnalysis/main/IMDB%20Dataset.csv", header=0)
```


```python
data=df.head(2000) # this subset is used for scattertext in step 3. If I use the whole data, the graph for the HTML that it generates will be two heavy to
```

---

**Step 3:**

Let's see what the data looks like. We can use the `head` function which returns the first 5 rows of the dataframe.


```python
# Print the first 5 rows of the data using head function of pandas
df.head()
```



There are 2 columns in the dataframe - `review` and `sentiment`. The `review` column contains the text of the review and the `sentiment` column contains the sentiment of the review.

The `describe()` function gives us a summary of the data.


```python
#Describe the data using describe function of pandas
df.describe()

```



We can see that we have 50,000 reviews in our dataset. The `sentiment` column has 2 unique values - `positive` and `negative`.

Individual columns can be accessed using the `[]` operator. For example, `df['review']` returns the `review` column of the dataframe.


```python
print(df['review'])
```

    0        One of the other reviewers has mentioned that ...
    1        A wonderful little production. <br /><br />The...
    2        I thought this was a wonderful way to spend ti...
    3        Basically there's a family where a little boy ...
    4        Petter Mattei's "Love in the Time of Money" is...
                                   ...                        
    49995    I thought this movie did a down right good job...
    49996    Bad plot, bad dialogue, bad acting, idiotic di...
    49997    I am a Catholic taught in parochial elementary...
    49998    I'm going to have to disagree with the previou...
    49999    No one expects the Star Trek movies to be high...
    Name: review, Length: 50000, dtype: object


Let's see how many positive and negative reviews we have in our dataset. We can use the `value_counts()` function to get the count of each unique value in the `sentiment` column.


```python
# Use the value_counts function to count the number of positive and negative reviews on the sentiment column using the [] operator
df["sentiment"].value_counts()
```




    positive    25000
    negative    25000
    Name: sentiment, dtype: int64



We can see that we have 25,000 positive reviews and 25,000 negative reviews in our dataset. They are evenly distributed and we do not have to worry about class imbalance.

[Follow this link to learn more about class imbalance](https://machinelearningmastery.com/what-is-imbalanced-classification/).


---

**Step 4:**
Let's take a short break from coding and do some reading that is imperative to understand the concepts of this project.


The **objective** of our machine learning model will be to predict the sentiment of a review given the text of the review. So, the model needs to learn the relationship between the text of the review and the sentiment of the review. Hence, this is a supervised learning problem where the input is text and the output is a label.

[Click here to watch introductory videos and learn more about supervised machine learning](https://www.youtube.com/playlist?list=PLNs9ZO9jGtUCiGTo3iP0qmI9_qi8oYaRN).



Since we are going to be using text as input, we cannot directly use the text because computers do not understand text. We need to convert the text into a format that is useful for our classification model.

Count vectorization is a method to convert text into a format that is useful for classification models. It converts the text into a matrix of token counts meaning that each row in the matrix represents a review and each column represents a word. The value in each cell is the number of times that word occurs in that review. So, by learning the frequency of each word in each review, the model can learn the relationship between the text and the sentiment of the review. The intuition behind this is that positive reviews will have more positive words and negative reviews will have more negative words.

Now that we have established the intuition behind count vectorization, let's look at features of the count vectorizer. The features of the count vectorizer are the words that we want to consider. We would only want to use words that are relevant to the sentiment of the review. For example, if we are classifying reviews of movies, we would not want to consider words like `the`, `a`, `an` etc. because they are not relevant to the sentiment of the review. Also, we would want to consider words that occur frequently in the reviews. For example, if a word occurs only once in the entire dataset, it is not very useful for our model.

To remove words that are not relevant to the sentiment of the review, first we need to tokenize the text.

Tokenization is the process of splitting a string into a list of tokens. This helps us to break down the text into smaller chunks which are easier to work with. What we essentially want to do  is remove all the punctuation and special characters from the text because they do not add any value to the text. We also want to convert all the text to lowercase so that the model does not treat the same word with different cases as different words.

---
---



<h3 align = "center">
    Milestone #2
</h3>

NOTE: These steps are to be completed **individually**, not as a team. You are encouraged to discuss steps with your teammates. Please attend Office Hours or ask your questions on Slack.

GOAL: The main goal of this milestone is to learn natural langauge processing and how to use the NLTK library to preprocess text. We will also learn how to use the CountVectorizer class to convert text into a format that is useful for classification models.

**Step 1:**

We will use the `nltk` library to perform these preprocessing steps. First, we will use the `word_tokenize` function to tokenize the text.


```python
# We apply the word_tokenize function to the reviews in the dataset and assign the tokenized reviews to the existing column in the dataset.
# We can use the apply function to apply the word_tokenize function to the reviews column in the dataset.
import nltk
nltk.download('punkt')
df['review'] = df['review'].apply(word_tokenize)
```

    [nltk_data] Downloading package punkt to /root/nltk_data...
    [nltk_data]   Unzipping tokenizers/punkt.zip.



```python
# We can see that the `review` column now contains a list of tokens for each review. Let's see what the first review looks like.
df['review'][1]
```




    ['A',
     'wonderful',
     'little',
     'production',
     '.',
     '<',
     'br',
     '/',
     '>',
     '<',
     'br',
     '/',
     '>',
     'The',
     'filming',
     'technique',
     'is',
     'very',
     'unassuming-',
     'very',
     'old-time-BBC',
     'fashion',
     'and',
     'gives',
     'a',
     'comforting',
     ',',
     'and',
     'sometimes',
     'discomforting',
     ',',
     'sense',
     'of',
     'realism',
     'to',
     'the',
     'entire',
     'piece',
     '.',
     '<',
     'br',
     '/',
     '>',
     '<',
     'br',
     '/',
     '>',
     'The',
     'actors',
     'are',
     'extremely',
     'well',
     'chosen-',
     'Michael',
     'Sheen',
     'not',
     'only',
     '``',
     'has',
     'got',
     'all',
     'the',
     'polari',
     "''",
     'but',
     'he',
     'has',
     'all',
     'the',
     'voices',
     'down',
     'pat',
     'too',
     '...']



We see that the text has been tokenized into a list of words. Also, the list contains punctuation and special characters which we do not want.

---

**Step 2:**


Let's clean the text by removing punctuations, special characters and converting the text to lowercase. We will use the `isalpha` function to check if a word is an alphabet. If it is not an alphabet, we will remove it from the list. We will also convert the text to lowercase using the `lower` function. Next, we will remove the stopwords from the list. Stopwords are words that do not add any value to the text. For example, `the`, `a`, `an` etc. are stopwords. We will use the `stopwords` function from the `nltk.corpus` package to get a list of stopwords. We will then use the `remove` function to remove the stopwords from the list.


```python
# isalpha() function returns True if all the characters in the string are alphabets. If not, it returns False.

# We can use the isalpha() function to remove all the punctuations and numbers from the reviews.

df['review'] = df['review'].apply(lambda x: [item for item in x if item.isalpha()])

```


```python
print(" ".join(df['review'][1]))
```

    A wonderful little production br br The filming technique is very very fashion and gives a comforting and sometimes discomforting sense of realism to the entire piece br br The actors are extremely well Michael Sheen not only has got all the polari but he has all the voices down pat too You can truly see the seamless editing guided by the references to Williams diary entries not only is it well worth the watching but it is a terrificly written and performed piece A masterful production about one of the great master of comedy and his life br br The realism really comes home with the little things the fantasy of the guard which rather than use the traditional techniques remains solid then disappears It plays on our knowledge and our senses particularly with the scenes concerning Orton and Halliwell and the sets particularly of their flat with Halliwell murals decorating every surface are terribly well done



```python
#TODO: convert to lowercase
#complete the code below
#df[''] = df[''].apply(lambda x: [item. for item in x])
df["review"]=df["review"].apply(lambda x: [item.lower() for item in x])

```


```python
print(" ".join(df['review'][1]))# the uppercase is converted to lowercase
```

    a wonderful little production br br the filming technique is very very fashion and gives a comforting and sometimes discomforting sense of realism to the entire piece br br the actors are extremely well michael sheen not only has got all the polari but he has all the voices down pat too you can truly see the seamless editing guided by the references to williams diary entries not only is it well worth the watching but it is a terrificly written and performed piece a masterful production about one of the great master of comedy and his life br br the realism really comes home with the little things the fantasy of the guard which rather than use the traditional techniques remains solid then disappears it plays on our knowledge and our senses particularly with the scenes concerning orton and halliwell and the sets particularly of their flat with halliwell murals decorating every surface are terribly well done



```python
df.head()
```





```python
# remove stopwords
import nltk
nltk.download('stopwords')
from nltk.corpus import stopwords
stop_words = set(stopwords.words('english'))

df['review'] = df['review'].apply(lambda x: [item for item in x if item not in stop_words])

```

    [nltk_data] Downloading package stopwords to /root/nltk_data...
    [nltk_data]   Unzipping corpora/stopwords.zip.



```python
df
```



---

**Step 3:**

Now that we have cleaned the text, we need to use a stemmer to stem the words. Stemming is the process of reducing a word to its root form. For example, the root form of the word `running` is `run`. Stemming helps us to reduce the number of unique words in the text. We will use the `PorterStemmer` function from the `nltk.stem` package to stem the words.


```python
# stemming user PorterStemmer

from nltk.stem import PorterStemmer
ps = PorterStemmer()

df['review'] = df['review'].apply(lambda x: [ps.stem(item) for item in x])

```


```python
df
```





```python
#join list of words to form sentences
df['review'] = df['review'].apply(lambda x: " ".join(x))
```


```python
df
```




---
---



<h3 align = "center">
    Milestone #3
</h3>


GOAL: The main goal of this milestone is to split the dataset into training and testing sets. We will also learn how to use the CountVectorizer class to convert text into a format that is useful for classification models. We will also learn how to use the MultinomialNB class to train a Naive Bayes classifier.

Training and Testing Data:

Machine learning uses algorithms to learn from data in datasets. They find patterns, develop understanding, make decisions, and evaluate those decisions.

In machine learning, datasets are split into two subsets:

The first subset is known as the **training data** - it’s a portion of our actual dataset that is fed into the machine learning model to discover and learn patterns. In this way, it trains our model.

The other subset is known as the **testing data**.

Once your machine learning model is built (with your training data), you need unseen data to test your model. This data is called testing data, and you can use it to evaluate the performance and progress of your algorithms’ training and adjust or optimize it for improved results.

Testing data has two main criteria. It should:

1. Represent the actual dataset
2. Be large enough to generate meaningful predictions


**Step 1:**

Now, the data is tokenized, cleaned and reduced to its root form.
The next step is to split the data for training and testing. We split the data because we need to train our model on some data and test it on some data. We have a total of 50,000 reviews, so let's split it into 40,000 reviews for training and 10,000 reviews for testing.
To do this, we can use the slice operator `:`. For example, `df[:30000]` returns the first 30,000 rows of the dataframe. Similarly, `df[30000:]` returns the last 20,000 rows of the dataframe.

Name the training data as `train_reviews` and testing data as `test_reviews`. Remember, we are only splitting the reviews column and will do the same for sentiment in the next step.


```python
#train reviews
train_reviews = df.review[:40000]
```


```python
#test reviews
test_reviews = df.review[40000:]
```

Now let us do the same for the sentiment column. Name the training data as `train_sentiments` and testing data as `test_sentiments`.


```python
#TODO: train sentiments
train_sentiments=df.sentiment[:40000]
```


```python
#TODO: test sentiments
test_sentiments=df.sentiment[40000:]
```


```python
test_sentiments.info()# to test if test dataframe takes the rest of the data
```

    <class 'pandas.core.series.Series'>
    RangeIndex: 10000 entries, 40000 to 49999
    Series name: sentiment
    Non-Null Count  Dtype 
    --------------  ----- 
    10000 non-null  object
    dtypes: object(1)
    memory usage: 78.3+ KB


---


**Step 2:**

We need to make a few changes to the data before we can use it to train our model. First, we need to convert the data into a format that is useful for our model. We will use the `CountVectorizer` function from the `sklearn.feature_extraction.text` package to convert the text into a matrix of token counts.

For the sentiment column, we need to convert the labels into numbers. We will use the `LabelEncoder` function from the `sklearn.preprocessing` package to convert the labels into numbers.

[To read more about Count Vectorizer, follow this link](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html). [You can also use this link to read more about Label Encoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html). Please go through the parameters of both these functions to better understand the code below.


```python
#Count vectorizer for bag of words
cv = CountVectorizer(min_df=0, max_df=1, binary = False, ngram_range = (1,3))
```

To transform the data, we will use the `fit_transform` function. The `fit_transform` function fits the model to the data and then transforms the data into a matrix of token counts. We will use the `fit_transform` function on the training data and the `transform` function on the testing data. This is because we only want to fit the model to the training data and not the testing data.


```python
#transformed train reviews
cv_train_reviews = cv.fit_transform(train_reviews)

```


```python
#transformed test reviews
cv_test_reviews = cv.transform(test_reviews)

```

Again, for the sentiment column, we will use the `fit_transform` function on the training data and the `transform` function on the testing data.


```python
#labeling the sentient data
lb = LabelBinarizer()
```


```python
# transformed sentiment data
lb_train_sentiments = lb.fit_transform(train_sentiments)

```


```python
#TODO: transformed test sentiment data (similar to count vectorizer, transform test reviews, name it lb_test_sentiments)
# Remember to use transform and not fit_transform
lb_test_sentiments=lb.transform(test_sentiments)

```

---

**Step 3:**

Model Building: In this step, we will build our model. We will use the `MultinomialNB` function from the `sklearn.naive_bayes` package to build our model. The Multinomial Naive Bayes classifier is suitable for classification with discrete features (e.g., word counts for text classification). The multinomial distribution normally requires integer feature counts. Bag-of-Word counts are an example of integer-valued discrete features.

[Please read about the Multinomial Naive Bayes classifier here](https://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.MultinomialNB.html) and write about it in the comments below.

<h4 style="color:orange">
    TO-DO
</h4>

Write a few lines about the following:

- **Machine Learning Classifiers:**

According to Mesevage (2020), a classifier in machine learning is an algorithm that automatically orders or categorizes data into one or more of a set of “classes.” One of the most common examples is an email classifier that scans emails to filter them by class label: Spam or Not Spam.

Dutta (2020) distinguished 6 classifiers:

 - **Perceptron**

  "It is one of the original and most basic forms of artificial neural networks. The author argues that it isn't "deep" learning, but it is a necessary building component. It is made up of a single node or neuron that processes a row of data and predicts a class label.

- **Logistic Regression:**  
  A logistic function is used to describe the probability of the probable outcomes of a single trial in this technique. Logistic regression was created for this goal (classification),and it's especially good for figuring out how numerous independent factors affect a single outcome variable.

- **Naive Bayes Classifier:**

  The same author argues that Naive Bayes family of probabilistic algorithms calculates the likelihood that every given data point falls into one or more of a set of categories (or not). It is a supervised learning approach for addressing classification issues that are based on the Bayes theorem.

- **K-Nearest Neighbor:**
 According to IBM (n.d.), the k-nearest neighbors algorithm, also known as KNN or k-NN, is a non-parametric, supervised learning classifier, which uses proximity to make classifications or predictions about the grouping of an individual data point. While it can be used for either regression or classification problems, it is typically used as a classification algorithm, working off the assumption that similar points can be found near one another.

Since it is not mentioned in the documents to write about the other classifiers, I will only list the two others let. They are the following:
- **Support Vector Machine**

- **Random Forest**


Mesevage, T. (2020). Machine Classifiers - The Algorithms and How they work.Monkey Learn. https://monkeylearn.com/blog/what-is-a-classifier/


Dutta, B. (2020). Six types of Classifiers in Machine Learning. EanalyticSteps. https://www.analyticssteps.com/blogs/types-classifiers-machine-learning

https://www.ibm.com/topics/knn#:~:text=The%20k%2Dnearest%20neighbors%20algorithm%2C%20also%20known%20as%20KNN%20or,of%20an%20individual%20data%20point.


The first part is to train and fit the Multinomial Naive Bayes classifier to the training data. We will use the `fit` function to train the model on the training data.


```python
# training the model
mnb = MultinomialNB()
```


```python
# fitting the model
mnb_bow = mnb.fit(cv_train_reviews, lb_train_sentiments)

```

    /usr/local/lib/python3.10/dist-packages/sklearn/utils/validation.py:1143: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples, ), for example using ravel().
      y = column_or_1d(y, warn=True)



```python
#Predicting the model for bag of words
mnb_bow_predict = mnb.predict(cv_test_reviews)


```


```python
#Accuracy score for bag of words
mnb_bow_score = accuracy_score(lb_test_sentiments, mnb_bow_predict)
print("Accuracy :", mnb_bow_score)
```

    Accuracy : 0.7425


If you have completed all the steps correctly, you should see an accuracy of ~70-80%. This is decent, but not a very good accuracy since language is a very complex thing. But it's a great start!

---
---

<h3 align = "center">
    Milestone #4
</h3>

NOTE: This milestone is to be completed as a **group**.  Each group member should try a different classifier and you must discuss the results with your teammates. Please attend Office Hours or ask your questions on Slack.

GOAL: The main goal of this milestone is to understand how to use different classifiers to train a model and how to evaluate the performance of the model.

**Step 1:**

<h4 style="color:orange">

</h4>

Let's understand the reason why we use the K-nearest neighbor.

**The K-nearest neighbor**

KNN stands for K Nearest Neighbour. It is a supervised machine learning algorithm that classifies the new text by mapping it with the nearest matches in the training data to make predictions. Since neighbours share similar behavior and characteristics, they can be treated like they belong to the same group. Similarly, the KNN algorithm determines the K nearest neighbours by the closeness and proximity among the training data. The model is trained so that when new data is passed through the model, it can easily match the text to the group or class it belongs to.


[Please read about the different classifiers here](https://scikit-learn.org/stable/supervised_learning.html#supervised-learning).
Each team member should try at least one **different** classifier. You can try more than one classifier if you want. Please write about the classifier you have chosen in the comments below.


```python
#Enter your code here
from sklearn.neighbors import (NeighborhoodComponentsAnalysis,KNeighborsClassifier)

# Create a KNN classifier
knn = KNeighborsClassifier(n_neighbors=2)
knnfit=knn.fit(cv_train_reviews, lb_train_sentiments)
# predicting the model
knnfit_predict=knn.predict(cv_test_reviews)
#Accuracy score for bag of words
knn_bow_score = accuracy_score(lb_test_sentiments, knnfit_predict)
print("Accuracy :", knn_bow_score)

```

    /usr/local/lib/python3.10/dist-packages/sklearn/neighbors/_classification.py:215: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples,), for example using ravel().
      return self._fit(X, y)


    Accuracy : 0.4993



```python
from sklearn.metrics import classification_report,confusion_matrix
visualiser=classification_report(lb_test_sentiments, knnfit_predict)
print(visualiser)
```

                  precision    recall  f1-score   support
    
               0       0.50      1.00      0.67      4993
               1       0.00      0.00      0.00      5007
    
        accuracy                           0.50     10000
       macro avg       0.25      0.50      0.33     10000
    weighted avg       0.25      0.50      0.33     10000
    


    /usr/local/lib/python3.10/dist-packages/sklearn/metrics/_classification.py:1344: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
      _warn_prf(average, modifier, msg_start, len(result))
    /usr/local/lib/python3.10/dist-packages/sklearn/metrics/_classification.py:1344: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
      _warn_prf(average, modifier, msg_start, len(result))
    /usr/local/lib/python3.10/dist-packages/sklearn/metrics/_classification.py:1344: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
      _warn_prf(average, modifier, msg_start, len(result))



```python
# confusion Matrix
print(confusion_matrix(lb_test_sentiments, knnfit_predict))
```

    [[4993    0]
     [5007    0]]


**Support Vector Machine**

According to DataCamp (2019), SVM offers very high accuracy compared to other classifiers such as logistic regression, and decision trees. It is known for its kernel trick to handle nonlinear input spaces. It is used in a variety of applications such as face detection, intrusion detection, classification of emails, news articles and web pages, classification of genes, and handwriting recognition.

According to the same source, Support Vector Machines is considered to be a classification approach, it but can be employed in both types of classification and regression problems. It can easily handle multiple continuous and categorical variables. SVM constructs a hyperplane in multidimensional space to separate different classes.
DataCamp (2019). Support Vector Machine Scikit Learn Tutorial. https://www.datacamp.com/tutorial/svm-classification-scikit-learn-python


```python
from sklearn import svm
import numpy as np
clf=svm.SVC(kernel="linear")

```


```python
clfds=clf.fit(cv_train_reviews, np.ravel(lb_train_sentiments))
#This is where I have a problem. Whenever I excute this line, it takes a lot of time and the execution never finishes.
# I was waiting for this to execute in order to predict the model and run the accuracy test.
```


```python
#Decision Tree Forest
gf=np.array(lb_train_sentiments)
gf
from sklearn import tree
clf=tree.DecisionTreeClassifier(random_state=0)
fdf=clf.fit(cv_train_reviews, gf)
```


```python
y_predict=clf.predict(cv_test_reviews)
```

---

**Step 2:**

Data Visualizations are a great way to understand the data. [If you are interested in finding additional resources on Data Visualization, we recommend leveraging the DSRR resources, linked here.](https://nebigdatahub.org/nsdc/data-science-resource-repository/) We will be using word clouds to visualize the data. Word clouds are a great way to visualize the most frequent words in a text. We will use the `WordCloud` function from the `wordcloud` package to visualize the most frequent words in the reviews.

[Please read about the WordCloud function here](https://amueller.github.io/word_cloud/generated/wordcloud.WordCloud.html).




```python
# word cloud for positive review words in the entire dataset
from wordcloud import WordCloud, STOPWORDS
import matplotlib.pyplot as plt
%matplotlib inline

#join all the positive reviews
positive_words = ' '.join(list(df[df['sentiment'] == 'positive']['review']))

#word cloud for positive words
wordcloud = WordCloud(width=800, height=500, random_state=21, max_font_size=110).generate(positive_words)

plt.figure(figsize=(10, 7))
plt.imshow(wordcloud, interpolation="bilinear")
plt.axis('off')
plt.show()


```


    
![png](NLP_Movie_Review_Analysis_Daniel_SINEUS%20%281%29_files/NLP_Movie_Review_Analysis_Daniel_SINEUS%20%281%29_99_0.png)
    



```python
# TODO: Word cloud for negative reviews in the dataset
#join all the negative reviews
negative_words=" ".join(list(df[df["sentiment"]=="negative"]["review"]))
#word cloud for negative words
wordcloud = WordCloud(width=800, height=500, random_state=21, max_font_size=110).generate(negative_words)

plt.figure(figsize=(10, 7))
plt.imshow(wordcloud, interpolation="bilinear")
plt.axis('off')
plt.show()

```


    
![png](NLP_Movie_Review_Analysis_Daniel_SINEUS%20%281%29_files/NLP_Movie_Review_Analysis_Daniel_SINEUS%20%281%29_100_0.png)
    


---

**Step 3:** (Extra Points: Optional!!)
If you are able to complete this step and the remaining ones correctly, we will endorse your data science skills on LinkedIn.

Make a visualization of your choice! This is your chance to show your creativity and read about different visualization techniques. You can use the `matplotlib` package to make a visualization of your choice. You can also use the `seaborn` package to make a visualization of your choice.


```python
# Create Visualization of y choice
sns.set(style="darkgrid")
sns.countplot(x="sentiment", data=df)
```




    <Axes: xlabel='sentiment', ylabel='count'>




    
![png](NLP_Movie_Review_Analysis_Daniel_SINEUS%20%281%29_files/NLP_Movie_Review_Analysis_Daniel_SINEUS%20%281%29_104_1.png)
    



```python


sns.countplot(y='sentiment',
             data=df,
             palette=['#b2d8d8',"#008080", '#db3d13']
             );
```


    
![png](NLP_Movie_Review_Analysis_Daniel_SINEUS%20%281%29_files/NLP_Movie_Review_Analysis_Daniel_SINEUS%20%281%29_105_0.png)
    



```python
!pip install tqdm # try to use tqdm to see the progress of the code execution being downloaded
```

    Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
    Requirement already satisfied: tqdm in /usr/local/lib/python3.10/dist-packages (4.65.0)



```python
from tqdm import tqdm

```

scattertext is a free, open-source library in Python.

**Scattertext** is particularly useful when:

* You want to visualize how words are distributed between two categorical variables.
* You want to create interactive scatter plots that display distinguishable terms in corpora.
* You want to find or order characteristics terms or phrases and their associations.


Reference:
 https://guides.library.upenn.edu/penntdm/python/scattertext


```python
!pip install scattertext # install the scattertext package
```

    
```python
# use scattertext
!pip install spacy


```

    Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
  

```python
import scattertext as st # import the packages for the scattertext
import spacy
from pprint import pprint

```


```python
import spacy
nlp =spacy.load("en_core_web_sm")
```


```python

# construct the corpus
with tqdm(total=len(data)) as pbar:#tqdm didn't work. I will learn more about how to use it
    corpus = st.CorpusFromPandas(data,
                                 category_col='sentiment',
                                 text_col='review',
                                 nlp=nlp).build()
```

      0%|          | 0/2000 [02:12<?, ?it/s]



```python
from google.colab import drive
drive.mount('/content/drive')
```


```python
print(list(corpus.get_scaled_f_scores_vs_background().index[:10]))
```

    ['cinematography', 'scenes', 'br', 'believable', 'actors', 'film', 'plot', 'flick', 'acting', 'movie']



```python
term_freq_df = corpus.get_term_freq_df()
term_freq_df['positive Score'] = corpus.get_scaled_f_scores('positive')
print(list(term_freq_df.sort_values(by='positive Score', ascending=False).index[:10]))
```

    ['excellent', 'wonderful', 'loved', 'perfect', 'performances', 'favorite', 'war', 'brilliant', 'definitely', 'amazing']



```python
# visualize with scattertext
# Create html visualization
html = st.produce_scattertext_explorer(corpus,
                                       category='positive',
                                       category_name='Positive',
                                       not_category_name='negative',
                                       width_in_pixels=500,
                                      minimum_term_frequency=10)

# Save the HTML visualization to a file
with open("Scattertext_Visualization.html", "w") as f:
    f.write(html)
```


```python
import webbrowser
# Open the HTML v
#visualization in a web browser
webbrowser.open("Scattertext_Visualization.html")

```




    False




```python
from IPython.display import display, HTML

# Read the HTML file
html_content = open("Scattertext_Visualization.html", 'r').read()

# Display the HTML content
display(HTML(html_content))

```
        

```python
from google.colab import files

# Download the HTML file
files.download("Scattertext_Visualization.html")
```



---
---

<h3 align = 'center' >
Thank you for reading this project!
</h3>

Please do reach out to us if you have any questions or concerns. We are here to help you learn and grow.



