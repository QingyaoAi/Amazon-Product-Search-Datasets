# Overview #
This is an benchmark dataset for personalized product search. Please cite the following paper if you plan to use it in any way：
    
*	Qingyao Ai, Yongfeng Zhang, Keping Bi, Xu Chen, W. Bruce Croft. Learning a Hierarchical Embedding Model for Personalized ProductSearch. In Proceedings of SIGIR ’17
    	
Also, because this benchmark is built with the 5-core data of Amazon review datasets provided by McAuley et al. [3,4] (http://jmcauley.ucsd.edu/data/amazon/), please cite one or both of their papers following if you use the data:

*	R. He, J. McAuley. Ups and downs: Modeling the visual evolution of fashion trends with one-class collaborative filtering. In Proceedings of WWW ’16
*	J. McAuley, C. Targett, J. Shi, A. van den Hengel. Image-based recommendations on styles and substitutes. In Proceedings of SIGIR ’15


### Data Descriptions ###

*	This dataset is built with the 5-core data provided by McAuley et al.[4] where each user and each item has at least 5 associated reviews.
*	In these datasets, a user has to purchase an item before writing a review for it, so the purchase user-item pairs were directly extracted based on user reviews. The objective of personalized product search is to find items that are both relevant to the query and purchased by the user.

### Query Extraction ###

The search queries for each item were extracted following the paradigm used by Gysel et al.[1]:
*	Category information for each item were extracted from the metadata of products, and the terms from a single hierarchy of categories were concatenated to form a topic string.
*	Stopwords and duplicate words are removed from the topic string.
*	The category hierarchies with only one level were ignored.
*	Duplicate words are removed sequentially from the first level of category hierarchy to the last level (e.g. "Camera, Photo -> Digital Camera Lenses" would be converted to "photo digital camera lenses").
*	For personalized product search, user-query pairs are constructed by linking user-item pairs with each item's queries. In other words, if a user purchased an item, the pairing of this user with any query associated with the item are valid user-query pairs, and the items that are purchased by the user and belong to the query are considered as relevant to the user-query pair.


### Data Partition ###
Each dataset is split into a training set and a test set according to the following instructions:
*	30\% of reviews are randomly hided for each user from the training process. User-item pairs from those reviews are used to represent purchase behaviors in the test data.
*	30\% queries are randomly selected as the initial test query set. If all queries of a training item are in the test query set, one query is randomly selected and put back to the training query set.
*	All test queries are matched with users to form the final test data.

### File format ###

Each directory is named after the orignal file name of the 5-core data provided by McAuley et al.[4]. The detailed format for each file in each directory is as follows: 
```
    1. query_text.txt.gz: # All queries used in training and testing.
    	Each line represent one query string.
	2. train.qrels.gz: # The relevance judgements of the training data.
    	<reviewerID>_<query_line_number> 0 <asin> <relevance_label>
    	<reviewerID>: the user id in the original 5-core data.
    	<query_line_number>: the line number (start from 0) of the query in query_text.txt.gz.
    	<asin>: the product id in the original 5-core data.
    	<relevance_label>: a binary label denoting whether the user has purchased the item after searching the query (1 for purchased and 0 for not).
    3. train_review_id.txt.gz: # the line id of the corresponding in the original 5-core Amazon review data
    	line_<review_line_number>
    	<review_line_number>: the line number (start from 0) of the review data in the original 5-core data.
    4. test.qrels.gz: # The relevance judgements of the test data
    	<reviewerID>_<query_line_number> 0 <asin> <relevance_label>
    	<reviewerID>: the user id in the original 5-core data.
    	<query_line_number>: the line number (start from 0) of the query in query_text.txt.gz.
    	<asin>: the product id in the original 5-core data.
    	<relevance_label>: a binary label denoting whether the user has purchased the item after searching the query (1 for purchased and 0 for not).
```

### Reference: ###
    [1] Christophe Van Gysel, Maarten de Rijke, and Evangelos Kanoulas. 2016. Learning latent vector spaces for product search. In Proceedings of CIKM '16.
    [2] Qingyao Ai, Yongfeng Zhang, Keping Bi, Xu Chen, W. Bruce Croft. 2017. Learning a Hierarchical Embedding Model for Personalized ProductSearch. In Proceedings of SIGIR ’17
    [3] R. He, J. McAuley. Ups and downs: Modeling the visual evolution of fashion trends with one-class collaborative filtering. In Proceedings of WWW ’16
	[4] J. McAuley, C. Targett, J. Shi, A. van den Hengel. Image-based recommendations on styles and substitutes. In Proceedings of SIGIR ’15