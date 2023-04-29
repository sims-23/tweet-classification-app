# tweet-classification-app

## Tutorials found here:
https://www.youtube.com/watch?v=S--SD4QbGps&list=PL_TPqZIua6E8FyTD_-8Ywdpqiid1EGIfq&index=2&t=239s&ab_channel=PythonEngineer
https://www.youtube.com/watch?v=zGP_nYmZd9c&ab_channel=FrancescoCiulla

## Dataset used:
https://www.kaggle.com/datasets/kazanova/sentiment140

## Why did I pick this tutorial?
To refresh and improve my Docker knowledge. Also, to learn how to transfer a notebook to a production ready web app created with Flask.

## Why it's important to know Docker?
Docker is one of the most popular containerization platform. 

Now you might be asking, what is containerization (or not, but I'm going to answer this anyways)?
Containerization is about creating a container. Okay, I'm done.

I'm just kidding. I'm also going to give you the definition of what a container is from the Docker website. "A container is a unit of software that packages up code and all its dependencies" (1). There are many reasons why we might want have this, but the main one being is that it gives us portability. If you've ever had the trouble of running app, wondering why it works on someone else's machine rather than your own, Docker helps to fix that issue. Docker isolates the app from the computing environment. So when you run the app in the container, whether you're on Windows or macOS, it should work.

### Why not use a virtual machine?
A virtual machine can solve this problem, but a virtual machine is costly as a virtual machine has it's own operating system inside of it. Docker however uses the operating system of whatever its on whether it's a server or computer. This makes it much lighter.

### What was covered in tutorial about Docker?
Creating a Dockerfile (Dockerfile is used to build the Docker img).
Created a docker-compose.yml
Built the image and then ran the container with "docker compose up --build" command.
Tested that containerized application worked (I used Insomnia)
Learned to store image on Dockerhub with "docker compose push".
Tried to used the image we just stored on Dockerhub after removing the images and containers locally.

## A little more about the model in this tutorial:

Although the tutorial itself did not go too much into the model it's using as it was more so about deploying an ML app, I did find a bit about the reasoning behind the use of these models here https://www.kaggle.com/code/stoicstatic/twitter-sentiment-analysis-for-beginners

One way I would change the notebook is to either use the stop words provided by nltk which one can find here, https://www.tutorialspoint.com/python_text_processing/python_remove_stopwords.htm#:~:text=Stopwords%20are%20the%20English%20words,the%2C%20he%2C%20have%20etc. 
Currently the list of stopwords in the notebook seems quite small.

In the preprocessing steps, I noticed the use of the nltk's Wordnet lemmatizer. I decided to do a bit more of a deep dive into this, and read about the difference between a lemmatizing and stemming here https://www.datacamp.com/tutorial/stemming-lemmatization-python and here https://www.engati.com/glossary/lemmatization. Lemmatizing is a slow process, but it's a rule-based approach which can lead to more accurate results than stemming (however it is might be good to look at the accuracy results for when a stemmer is used versus a lematizer. If both work relatively the same, it might be better just to use the stemmer. This thought came about while reading https://www.kdnuggets.com/2019/04/text-preprocessing-nlp-machine-learning.html).

Another interesting thing was the TF-IDF Vectorizer. 

### Firstly, what are tf-idf values? 
They are good for determining the relevance of a word in a document. The higher the value is, the more relevant the term is to a document.

The "tf" part of "tf-idf" stands for "term frequency". It is exactly what it sounds like. It measures the frequency of a term. Although there are different ways term frequency can be defined, sklearn defines it as the number of times a term occurs in a document. 

But with "tf" by itself, we are giving importance to frequent unimportant words to a document like "a" or "the" when we might not want to. 

So what do we do? This is where the "idf" part comes in. The "idf" part stands for "inverse document frequency". It looks at a term against the corpus (group of documents) and determines how common it is amongst the corpus. If this value is close to 0, then the word appears in many documents and vice versa. We multiply this value by the "tf" and decreasing the weight of unimportant words and increasing the weights of important words.

The TF-IDF Vectorizer then just converts a collection of raw documents into a matrix of tf-idf matrix. Our TF-IDF Vectorizer takes into consideration unigrams and bigrams with up to 500000 features.

## What else happened in this tutorial?
This tutorial also looked at the evaluations of three models for this classification task. Particularly the Bernoulli Naive Bayes, Linear Support Vector Classification, and Logistic Regression. For the purpose of this tutorial, I think this sufficed. However, further exploration can always be done. 

We ended up setting up and saving a pipeline. 
Eventually we ended up importing the code needed from the notebook and created a predict function with our pickled model. 
After we created a Flask App where we can send a post request with some tweets in the format of JSON data. 

Sources
(1) https://www.docker.com/resources/what-container/

More Sources
https://www.ibm.com/cloud/architecture/content/course/containers-and-docker/docker-containers/
https://www.analyticsvidhya.com/blog/2021/11/how-sklearns-tfidfvectorizer-calculates-tf-idf-values/
https://www.capitalone.com/tech/machine-learning/understanding-tf-idf/
https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html


