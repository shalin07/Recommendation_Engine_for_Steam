# Recommendation_Engine_for_Steam
Recommending games for Steam
Developed by 
1) Shalin Barot
2) Michal Lyskawinski
3) SHrawan Sapre

In broad terms, recommender systems are based on two strategies;

1)Content Filtering - creates a profile for each user or product to characterize its nature

2)Collaborative Filtering - analyzes relationships between users and interdependencies among products to identify new user-item associations.

Our dataset contains records of previous transactions and behaviors of users and hence, we implemented the collaborative filtering approach and analyzed similar user purchases behaviors to predict which game a user would most likely purchase in the future.
The two primary areas of collaborative filtering are neighborhood methods and latent factor models. Neighborhood methods are based on computing the relationships between items or, alternatively, between users. The item-oriented approach evaluates a user’s preference for an item based on ratings of other “neighboring” or similar items. Latent factor models are an alternative approach that tries to explain the ratings by characterizing both items and users on several factors inferred from the purchase patterns.

Some of the most successful realizations of latent factor models are based on matrix factorization. Matrix factorization characterizes both items and users by vectors of factors inferred from item/user features. High correspondence between item and user factors leads to a recommendation. These methods have become popular in recent years by combining good scalability with predictive accuracy. In addition, they offer much flexibility for modeling various real-life situations.

One strength of matrix factorization is that it allows incorporation of additional information. When explicit feedback is not available, recommender systems can infer user preferences using implicit feedback, which indirectly reflects opinion by observing user behavior including purchase history, browsing history, search patterns, or even mouse movements. Implicit feedback usually denotes the presence or absence of an event, so it is typically represented by a densely filled matrix.

Our dataset involves user behavior that includes information corresponding to the number of hours a user has played a game and whether he has only purchased the game and not played it. Since no explicit feedback like “ratings” is present, we infer user preferences using implicit feedback that is binary. ‘1’ if a user has purchased a game and ‘0’ if a person has not purchased a game. From further data analysis of the data, we can also infer that a substantial sample of the population has only purchased the game and not played it at all. 

For recommending new games to a user, we formulated that a basic recommender model could be built only taking the purchase history into consideration. 

Our Model
We mapped the data to a joint latent factor space of dimensionality d*n, such that the user-item interactions are modeled as inner products in the space. Each user is associated with a vector pu Rd and each item is associated with a vector qiRn. 
For a given game i, the elements of qi measure the extent to which a game was played by users  pu. Similarly, for a given user u, the elements of pu measure the extent of interest the user has in the game (in this case we have a binary value: 1 for purchase, 0 for not purchased). 
The resulting dot product qiTpu captures the interaction between the user u and the game i. 
We get an approximation of the user u’s rating of a game i which is denoted by:
                                                                                r^ui = qi^Tpu                       			(1)

The model closely represents Singular Value Decomposition. At a high level, SVD is an algorithm that decomposes a matrix M into into two unitary matrices (U and Vt) and a diagonal matrix S:
                                                     M = USV^T					                                                  (2)
where M is user-game purchases matrix, U is the basis matrix, S is the diagonal matrix of singular values (essentially weights), and VT is the “features” matrix. U represents how much users “like” each feature and VT represents how relevant each game is to the user.
A sparsification technique is then applied to approximate  the rank of matrix M, namely the authors utilized thresholding by parameter “k” on the diagonal matrix S to remove not-meaningful representations.  Furthermore I tuned the parameter “k” to increase or decrease the number of r user-havioral groups. 
Then I recomposed M utilizing equation (2) to obtain final recommendation matrix R. 

Testing and Results:

For testing the recommendation engine I used random uniform sample of 2000 unique users who have purchased and played minimum of “d” games in other to reduce intrinsic randomness of recommending a single game based on a single feature. We made sure that all 2000 users selected for testing are unique. Then we selected “n” random game for every user in the testing group and altered their behavior by removing those “n” game purchase from the main matrix R. Then I checked, if the removed games appeared in the recommended set of “f” games. Then the mean of all of the recalls has been computed to arrived at global recall. Finally through hyper-parameters (k, n, d, f) tuning I arrived at global recall of  28% by setting k=101, n=2, d=10, f = 100 . (k value of 101 allows for rank of 23).


Conclusion and Remarks
When we made 155 groups of similar users I obtained recall of 5% then, then they tried for 50 groups of similar users and obtained got recall of 12% and then they made 20 groups of similar users where they got maximum accuracy of 22.15%. What surprise me, even though the data set includes around 12 thousand unique users, the are only 20 unique group in the data set, which means that vast majority of users usually play similar games.  
I believe that the recommendation system can be further improved by incorporating more features into the system like games genre, hours played and game type.
