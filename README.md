# Discriminative Topic Mining via Category Name Guided Text Embedding (CatE)

This repository is for CS 598, Jiawei Han's graduate level course in text mining at the University of Illinois at Urbana-Champaign.

## Problem Description

Traditional topic modeling could suffer from non-informative topics and overlapped semantics between different topics. As a response, discriminative topic mining incorporates user guidance as category name and retrieve representative and discriminative phrases during embedding learning. In the meantime, these category-name guided text embeddings can be further utilized to train a weakly-supervised classifier in high quality.

To train our weakly-supervised classifier, we can follow these four steps:

1. Download training dataset on news and movies (located in the `data` folder) and use `AutoPhrase` to extract high quality phrases.
2. Write or adopt [CatE](https://github.com/yumeng5/CatE) on segmented corpus to find representative terms for each category.
3. Perform weakly-supervised text classification with only class label names or keywords. For this, we will use [WestClass](https://github.com/yumeng5/WeSTClass)
4. Test your method on two datasets. Investigate their output and submit your result.


## Step 1: Adopt AutoPhrase to extract high quality phrases 

In this step, you will need to utilize AutoPhrase to extract high quality phrases in train.txt of both datasets provided. The extracted phrase list look like (the example here is different from homework test data):

Score     Phrase

0.9857636285     lung nodule
0.9850002116     presidential election
0.9834895762     wind turbines
0.9834120003     ifip wg

## Step 2: Compute category name guided embedding on segmented corpus

Use your segmentation model to parse the same corpus, recommended parameters for segmentation is  HIGHLIGHT_MULTI=0.7 HIGHLIGHT_SINGLE=1.0. An example segmented corpus can be:

An overview is presented of the use of spatial data structures in spatial databases. The focus is on hierarchical data structures, including a number of variants of quadtrees, which sort the data with respect to the space occupied by it. Such techniques are known as spatial indexing methods. Hierarchical data structures are based on the principle of recursive decomposition.

Then you will write your own cate or refer the existing ones to compute the phrase embedding as well as category-guided phrase mining. You will need to submit category and their top-10 representative terms in category_name_terms.txt. 

For example, in technology_terms.txt, you want have the first line as category name embedding, the following 10 lines would be category representative term embeddings

technology 0.720378 -0.312077 0.811608 ... 1.096724

terms_of_usage_privacy_policy_code_ 1.439691 0.508672 -0.958150 ... -1.277346

...

Tip: You can concatenate train.txt and test.txt into a larger corpus for phrase mining and category-named guided embeddings.

## Step 3: Document Classification with CatE embeddings  

In this step, you will need to build a weakly-supervised classifier (e.g. WestClass) on top of the term embeddings you obtained from the previous steps. The only supervision is category names provided in the datasets.

For example, in news, we have following category names in news_category.txt 

politics
sports
business
technology

To help validate your results, we also provide labels of first 100 documents in both dataset in news_train_labels.txt and movies_train_labels.txt. 

Tip: You can try label names or expanded keywords from the cate embeddings as weak supervision. We suggest you try both ways and report the better one.


## Step 4: Submit your result

In this step, you will apply both methods you implemented in Step 2 and Step 3 on two real-world datasets. Here are the detailed files when you downloaded the data.

News
	

120000
	

news_category.txt
	

news_train.txt
	news_test.txt	first 100 of news_train_labels.txt

Movies
	

25000
	

movies_category.txt
	

movies_train.txt
	movies_test.txt	first 100 of movies_train_labels.txt