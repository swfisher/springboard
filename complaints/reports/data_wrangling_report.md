# Extracting Value from Customer Complaints
## Data Wrangling Report

For this project I am using a publicly available dataset of complaints against financial institutions published by the Consumer Financial Protection Bureau. The dataset is luckily very clean and high quality, making the task of preparing it for exploration and modeling very straightforward.

The data is available as csv file from the [CFPB website](https://www.consumerfinance.gov/data-research/consumer-complaints/). After obtaining it and loading it into a pandas DataFrame, I found that the DataTypes had not been correctly inferred by default. In order to resolve this, I created a dict with the correct DataTypes and passed it to the astype method of the DataFrame.

The standard datetime parsing for pandas turned out to be a little slow when processing the entire DataFrame, so I found a solution on stack overflow using memoization to store and look up previously converted dates. This way each unique date only needed to be converted once and previously converted ones are simply referenced in a dictionary. 

The first aim of this project is the classify the issue expressed in a message based on it's text. To distill the relevant data, I took only the subset which had text available and removed the column which noted whether text was available.

Since the 'Bank account or service' topic seemed to have a fairly well balanced set of issue classes, I picked it to work with first. I created a copy, rather than a view, taking only the messages particular to this 'Topic.'

To derive quantitative information from the content of the complaints' text, I needed a strategy for creating meaningful vectors from them. To do this I created a 'Bag Of Words', which is a matrix representing the frequency of occurence of particular terms in each document. Notably, this throws all information regarding the placement of those words within the message. 
I chose this expecting to find meaninful semantic differences without using syntactical contex.
I utilized scikit-learn's CountVectorizer in order to create a bag of words matrix in which each topic was considered a document.

After experimenting with vectorizing the messages, I found that a few data preparation steps would be helpful on the text data. Redacted private information in the data set was noted by sequences of 'X' characters that did not correspond to the length or any other meaningful aspect of the redacted word.I simply removed these using a regular expression and the re library's sub method, applied to the DataFrame with DataFrame's apply method.

Since many of the algorithmically chosen word vectors contain meaningful numbers, I would like to proceed with finding a way to better parse these values in order to create meaningful groupings that result in more predictive and generalizable features in the extracted bag of words vectors.

