# Data Preparation
The dataframe consists of reviews from Amazon. 

Data downloaded from [Kaggle amazon reviews](https://www.kaggle.com/datasets/bittlingmayer/amazonreviews).

## About Data 


Amazon Review Full Score Dataset (from the README file downloaded from 
[here](https://www.kaggle.com/datasets/bittlingmayer/amazonreviews))

Version 3, Updated 09/09/2015

**ORIGIN**

The Amazon reviews dataset consists of reviews from amazon. 
The data span a period of 18 years, including ~35 million reviews up to March 2013. 
Reviews include product and user information, ratings, and a plaintext review. 
For more information, please refer to the following paper: J. McAuley and J. Leskovec. 
Hidden factors and hidden topics: understanding rating dimensions with review text. RecSys, 2013.

The Amazon reviews full score dataset is constructed by Xiang Zhang (xiang.zhang@nyu.edu) 
from the above dataset. It is used as a text classification benchmark in the 
following paper: Xiang Zhang, Junbo Zhao, Yann LeCun. Character-level Convolutional 
Networks for Text Classification. Advances in Neural Information Processing Systems 28 (NIPS 2015).


**DESCRIPTION**

The Amazon reviews full score dataset is constructed by randomly taking 600,000 
training samples and 130,000 testing samples for each review score from 1 to 5. 
In total there are 3,000,000 trainig samples and 650,000 testing samples.

The files train.csv and test.csv contain all the training samples as comma-sparated values. 
There are 3 columns in them, corresponding to class index (1 to 5), review title and review text. 
The review title and text are escaped using double quotes ("), and any internal double quote 
is escaped by 2 double quotes (""). New lines are escaped by a backslash followed with an "n" character, that is "\n".


**DATA PROCESSING**

The input data used is in the following format:
Id | ShortReview | ReviewContent 
--- | --- | ---
001 | Text | Review Description 
011 | Text | Review Description

 
Since the above dataset does not have any other information, except the text from the reviews, 
the follwoing columns are added to make the data more realistic.
- Index: unique ID
- Date: a randomly generated datetimestamp, YYYY-MM-DD HH:mm:ss (e.g. 2021-05-07 05:10:34)
  between 2020/05/09 and 2023/03/25 (these can be changed accordingly)
- ProductName: name of the product being reviewed. This is created by concatanating "productname" with the existing Id column.
- Category: randomly generated choice between 4 values, implying the category the product would belong to.
  This could be also thought as a Business Vertical or Location/Region.
  Only constraint - preferably not more than 5-6 values, as that would increase the computing time
  for the topic modeling. Details discussed in Topic modeling notebooks.

The output is following format.

Index | Date | ProductName | ReviewRate | Price | Category | ReviewContent 
--- | --- | --- | --- | --- | --- |---
001 | 2020-09-27 09:11:04 | name1 | 3.5 | 62.36 | Category1 | Text Description
011 | 2022-12-13 15:00:54 | name2 | 5 | 219.08 | Category2 | Text Description

This data is saved as a Table in the Hive Metastore.
