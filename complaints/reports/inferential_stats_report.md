# Extracting Value from Customer Complaints
## Inferential Statistics for Topic Classification

The first step I decided to undertake in order to algorithmically derive value from customer complaints was to classify the complaints by meaningful topics. Given such topics, we can analyze the average sentiment and frequency relative to other topics of complaint. 

The Consumer Financial Protection Bureau's dataset comes nicely labeled with Products, sub-products, issues, and sub-issues. Since I was more interested in classifying issues than products, I chose the banking product because it featured at least a few hundred example documents for every topic class.

A traditional classifier for this kind of task relies on the hypothesis that the distribution of how often words occur in a text will be predictive of the target class. In order to analyze whether this is the case, I initially computed tfidf scores that looked at 500 examples from each class as individual documents. The idea was that inverse document frequency would discount the term frequency in such a way that the most prevalent and specific words would reveal themselves.

While this was roughly the case, I later came to a much more straightforward way of finding out what ought to be predictive of the text's class. I first computed the tfidf values for a balanced sample of the classes, so that common terms would be appropriately discounted. I then computed the chisquared statistic for each term relative to each class. This statistic better approximated what I was hoping to do with class-level tfidf scores, it allowed me to analyze which terms were most highly correlated with each class. 

Printing out the first hundred of these words and scanning them gives a qualitative sense of how uniquely predictive certain key terms might be in classifying the document. By looking at the intersection of the high chisquared values, one can get a sense of where confusion between classes might emerge in a typical algorithm.

Our primary interest is in the seperability of these distinct classes in the feature space. The sense in which the chisquared values, computed in this way, give us insight into the that seperability between classes is limited. Given our rather expansive 15,000 features, each representing a word, discribing this seperability without applying some sort of learning model seems tough. I'm very interested to learn if such approaches exist and will proactively seek them out.         

