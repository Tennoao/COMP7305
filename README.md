# COMP7305  Cloud computing and cluster

Movie Recommendation Based on Spark:

Group15:
	HE ZHAOXUAN 	3035561699
	LI NI 		3035141322
	XUE BOTU 	3035562332
	FUNG KA YUE 	3035074634

***********************************************************************
1. What is the project about?

	Ans: This project applies Movie Recommendation in Apache Spark. 3 rating datasets from different movie recommendation websites (IMDB, TMDB, MOVIELENS) are collected and merged to build a movie recommendation engine. The engine is built in Apache Spark using the Alternative Least Squares algorithm.
**************************************************************************************
2) What are the datasets about?

	a) movie_pure_small.csv
	b) movie_pure_middle.csv
	c) movie_pure_large.csv
	d) movie_name.csv
	e) person.csv

	The first 3 datasets are rating datasets with different sizes.  movie_pure_large.csv is the full datasets with all rating records from the 3 sources. The format of the rating dataset is:
	userID(int),movieID(Int),rating(float)

	movie_name.csv is a mapping file of movieId and movie names. It is used to convert movieId into movie names when the output is printed on the shell.

	person.csv is a dataset which contains the rating for a new user.
************************************************************************************
3) What is the flow of the codes?

	a) A csv file is generated after a new user makes a rating. The csv file has the same format as the rating dataset:
	userId(Int),movieID(Int),rating(float)

	b) The csv file is pushed into the HDFS by typing:
	hdfs dfs -put /user/hduser

	c) Run model-based-movie-recommendation-person.py by typing (Persons.csv must be in the same folder as the py file):
	/opt/spark-2.4.0-bin-hadoop2.7/bin/spark-submit --master=yarn model-based-movie-recommendation-person.py persons.csv

	The py file will generate a new model that contains the new user rating and push the new model into HDFS.

	d) Run model-based-movie-recommendation-load-model.py by typing:
	/opt/spark-2.4.0-bin-hadoop2.7/bin/spark-submit --master=yarn model-based-movie-recommendation-person.py [userID of new user]

	The py file will load the model and recommend 10 top movies with the highest rating to the new user.

	Alternatively, model-based-movie-recommendation-RMSE can also be run by typing:
	/opt/spark-2.4.0-bin-hadoop2.7/bin/spark-submit --master=yarn model-based-movie-recommendation-RMSE.py
	This file helps generate the RMSE of the model.
