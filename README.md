# Anime CRP
## Anime Classifier, Recommender, Predictor
### Authors :
1. Eanumula Eswar Sai Yashwanth
2. Ram Kiran Devireddy
3. Gowri Shankar Badugu

### project-eeanumul-radevir-gbadugu

### Abstract

Models which are automated algorithms like classifiers and recommenders are used frequently nowadays. The use of data classifiers and recommenders which are used to analyze large data sets, to classify the data in it and to recommend something out of it are applied in many fields. One of those applications is Anime CRP (Anime Classifier, Recommender and Predictor) which uses the anime data set and classifies the data in it and recommends anime to user. This will be useful in entertainment field. Firstly, the Classifier classifies the anime based on a given category and suggests whether a given anime is recommended to the user or not. Secondly, using the above classifier along with clustering, the dataset can be grouped as Beginner, Pro, and Advanced based on number of episodes and genre to enable categorial recommendation. Thus, the Recommender recommends multiple groups of anime to watch for a user based on his/her preferences like genre, number of episodes, popularity, and ranking. Here, the recommender is designed based on a data mining classification algorithm called K-Nearest Neighbors (KNN) and on the other hand, the classifier is designed with a data mining clustering algorithm called K-Means Clustering. Finally, the future developments of this project would be building an anime predictor (predicting the anime a given user will be watching next) with the help of association rules.


### Dataset
[Link to our dataset](https://www.kaggle.com/datasets/marlesson/myanimelist-dataset-animes-profiles-reviews)

Data on user preferences for about 16,214 anime, collected from 47k individuals, are included in this data set. This data set also includes a collection of the user ratings of about 130k for each anime that they have added to their completed list. Thus, though this dataset, we’ll get the information related to anime (genre, rating, type, popularity etc.) and info related to user’s anime watch history (anime watch history of the users).
•	According to Kaggle, this dataset was pulled from myanimelist.net API.
•	anime.csv
1.	u_id: a unique identification number to differentiate each anime. More like anime_id.
Sample values: 1, 5, 6, 9 …...,40960 
2.	title: contains complete name of the anime. More like name.
Sample values: One Piece, Naruto, Fullmetal Alchemist etc
3.	synopsis: shows the summary of that particular anime.
4.	genre: gives us the information about which genre the anime belongs to.
Sample values: ['Sci-Fi', 'Shounen', 'Adventure', 'Mystery', 'Drama', 'Fantasy'] etc
5.	aired: range of date showing the starting and ending dates of anime.
Sample values: Oct 4, 2015, to Mar 27, 2016
6.	episodes: tells us the number of episodes the anime contains.
Sample values: 1, 64, 1015 etc
7.	members: shows the community of the anime
8.	popularity: an evaluation metric of the anime showing the popularity of the anime among the anime community.
9.	ranked: rank of the anime among other anime

### Methods

#### Classifier:

An algorithm that uses Anime Dataset which is used to design classifier and recommender is proposed to classify the anime data and recommend the anime to the user to watch based on the data present in the dataset. The methods used to classify and recommend are KNN and K-Means clustering with specified K values. 

##### Implementation of KNN:

1. Implementation of KNN. User also specifies how many anime i.e., K value such that k number of anime will be recommended.  User inputs the preferences of his/her through list of metrics like genre, popularity, number of episodes, and rank of the anime. Based on these preferences, the recommender algorithm does the following things,
•	Calculates how many genres of that anime matched with the user genre preferences and calculates the distance from that anime to unlabeled record.
•	Considers the popularity of that anime as 0 if the given popularity is more than respective anime popularity otherwise it is considered as 1.
•	Considers the rank of that anime as 1 if the given rank is more than respective anime’s rank otherwise it considers are 0.
•	Episodes will be considered as it is.
•	Then, it calculates the distance between all the anime’s and to that unlabeled record.
l_euclidian_distance = ((given preferences count – matched preferences count) **2) **0.5  + ((given_popularity – (1or 0))**2)**0.5 + ((given_rank– (1or 0))**2)**0.5 + ( (given_episodes – anime’s episodes)**2)**0.5

##### Categorial Recommender:

###### Clustering Objective:

Our aim for clustering is to build a categorial recommender. The user should get a recommendation of best or top anime in a certain category. Based on the popularity and rating, can we group the anime into best, worst and avg? Clustering would help us in building a recommender which can answer questions like ‘what are the best / top anime with less than 500 episodes?’. Below, we’ll be trying to build a recommender using k means clustering algorithm.

###### Implementing K means clustering:

1. Selecting the number of clusters/centroids ‘k’: Firstly, how many clusters do we need? We wanted to cluster the anime based on episodes like, beginner with number of episodes less than or equal to 100, pro anime with number of episodes less than equal to 500 and all the other anime with episodes greater than 500 as advanced. Please make a note that the maximum number of episodes for an anime in our data set is 3057. 
2. As we need 3 clusters, we’re selecting 3 centroids (k = 3). 50 for beginner anime, 250 for pro anime and 3057/2 for remaining anime.
3. Euclidean distance: Using the above centroids, we calculated Euclidean distance with every anime episode counts. 
4. As there were few ongoing anime, the episode counts for that anime were not populated, resulting in the null fields in distances. Thus, we replaced the null distances with the mean of the distances.
5. Clustering based on above distance: Using the distances we calculated above, we clustered the anime with shortest distance to centroid i.e., Anime episodes count closest to the centroids (50 or 250 or 3057/2).
6. Applying the K means clustering: To the above distances we got along with the episode’s column, we applied K means clustering.

#### FUTURE SCOPE
##### Predictor:

Will we be able to predict the anime a given user is going to watch next? Additionally, we can also build a predictor through the same Anime recommendation dataset. In the Anime recommendation dataset, we have a file named ‘rating.csv’ which contains the data of user rating to each anime. This dataset can be used as a data which shows us the group of anime watched by each user. By using this user anime watch history if we can find the frequently watched anime sets, we will be able to form association rules with it. Thus, after the association rules were set, if we get a user and his previous watched anime, we might be able to predict the anime he is most likely to watch next.

Example: Lets understand this better with the help of an example.

Let’s say that we got a user with anime watch history as {Naruto and Bleach}. Now let’s consider the below sets as few of the frequent anime sets, we got from the data set
•	{Naruto, Attack on Titan, One Piece}
•	{Boku No Hero Academia, Demon Slayer, Bleach}
•	{Full Metal Alchemist, Bleach, DBZ}
•	{Naruto, Bleach and One Piece} with some x confidence and y support.

Thus, from the above we can say that the user is more likely to watch One Piece next as he watched Naruto and Bleach. Like many other users who watched Naruto followed by Bleach and then One piece, our user might also watch One Piece Next.
Therefore, using the prior knowledge of users watch history, if we can build the association rules and form frequent anime watch sets, we can predict the anime a given user might watch next. This feature will be useful for any anime streaming services or platforms.

