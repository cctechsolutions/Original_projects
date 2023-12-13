# Unsupervised Machine Learning
## Clustering algorithms to segment customers by attributes and purchasing habits

<img src="./additional_files/images/priscilla-du-preez-YVssGmsSFhE-unsplash.jpg" width='700'>

*Companies who understand their customers and their behavior have an advantage over their competitors.  These understandings help companies know what messages will resonate with them and how to attract and retain these customers.  Insights into customers and purchase behavior can also help companies know how to attract certain types of customers and increase certain types of purchase behavior.  As of 2022, e-commerce accounts for nearly 19% of all purchases, and this is expected to continue increasing over the next few years.[^1]  Our client, a grocery store chain, wants to use these types of insights to increase online purchases from their customers.*

# Method

1. **Project proposal:**  Suggested plan for research methods and objectives

2. **Data wrangling:**  Found, imported, cleaned, and transformed data to prepare for analysis

3. **Exploratory data analysis:**  Examined the dataset to find patterns and insights and created graphics to visualize the data

4. **Develop machine learning algorithms:**  Created, evaluated, compared, fine-tuned, and improved models to determine which was best in this context

5. **Modeling:**  Used the chosen model to create clusters of the business's customers
   
6. **Conclusions and recommendations:**  Examined the resulting clusters and recommended future business actions

 &nbsp;   
***Final model:   KMeans clustering***
     
The algorithm that performed best and created the most useful clusters of customers was a KMeans clustering algorithm.  These clusters are created by examining the distance between each data point, which represents individual customers, and grouping those points that are the closest to each other into one algorithm and those that are farthest into different clusters.  Closeness is distance represents customers that have the most similarities in the attributes contained in this data, while points that are farther away show less similarity between customers.  When a clustering model performs well with the data it's given, the model results in clusters that are dense and distinct.  This is the case for the model we developed in this project.

# 1. Data   

“Customer personality analysis” dataset created by Dr. Omar Romero-Hernandez and uploaded to kaggle by Akash Patel 

[Original dataset from Kaggle](https://www.kaggle.com/datasets/imakash3011/customer-personality-analysis)

### About the dataset:
This is a 220.19 kB public domain csv file containing 2240 observations with the following 29 variables:
### People
* ID: Customer's unique identifier    
* Year_Birth: Customer's birth year    
* Education: Customer's education level     
* Marital_Status: Customer's marital status    
* Income: Customer's yearly household income     
* Kidhome: Number of children in customer's household     
* Teenhome: Number of teenagers in customer's household     
* Dt_Customer: Date of customer's enrollment with the company    
* Recency: Number of days since customer's last purchase    
* Complain: 1 if the customer complained in the last 2 years, 0 otherwise     
### Products
* MntWines: Amount spent on wine in last 2 years     
* MntFruits: Amount spent on fruits in last 2 years     
* MntMeatProducts: Amount spent on meat in last 2 years    
* MntFishProducts: Amount spent on fish in last 2 years    
* MntSweetProducts: Amount spent on sweets in last 2 years    
* MntGoldProds: Amount spent on gold in last 2 years    
### Promotion
* NumDealsPurchases: Number of purchases made with a discount    
* AcceptedCmp1: 1 if customer accepted the offer in the 1st campaign, 0 otherwise    
* AcceptedCmp2: 1 if customer accepted the offer in the 2nd campaign, 0 otherwise    
* AcceptedCmp3: 1 if customer accepted the offer in the 3rd campaign, 0 otherwise     
* AcceptedCmp4: 1 if customer accepted the offer in the 4th campaign, 0 otherwise     
* AcceptedCmp5: 1 if customer accepted the offer in the 5th campaign, 0 otherwise    
* Response: 1 if customer accepted the offer in the last campaign, 0 otherwise       
### Place
* NumWebPurchases: Number of purchases made through the company’s website     
* NumCatalogPurchases: Number of purchases made using a catalog    
* NumStorePurchases: Number of purchases made directly in stores     
* NumWebVisitsMonth: Number of visits to the company’s website in the last month      

# 2. Data wrangling    
[Data wrangling notebook](2_data_wrangling_3_eda.ipynb)

In a collaborative-filtering system there are only three columns that matter to apply the machine learning algorithms: the user, the item, and the explicit rating (see the example matrix above). I also had to clean & normalize all the reference information (location, difficulty grade, etc.) to the route so that my user could get a useful and informative recommendation.

* **Problem 1:** Missing values:  24 of the 2240 rows contained a missing value for the column income.  Before changing or removing these observations, I wanted to be sure that there are not any trends among these values that might affect our analysis.  I compared the rows that had a missing value with the averages of all other rows for each variable.  There was not a significant difference between other rows and those with missing values.  **Solution:** I imputed the missing income values with the mean value for income across the dataset.

* **Problem 2:** Some values given for categorical variables were in a different format than others.  Some appeared to be added as a joke, such as the values "Absurd" and "YOLO" in the column for relationship status.  **Solution:** For the education variable, I looked for information to learn which of the unknown labels were most equivalent to the education system in the US, as that is what I am most familiar with.  I then replaced the terms, "Basic," "2n cycle," with "High School" and "Masters" so that the format was the same across all observations.  I dropped the rows with "Absurd" and "YOLO" for relationship status as I had no way to determine what the true response should have been, nor was there any average value for that feature that I might use to impute them.

* **Problem 3:** There were more features than we would use for our analysis. **Solution:** While I did drop columns such as customer ID number, for many of the rather than simply dropping rows that we were not going to use, I instead combined rows

# 3. Exploratory data analysis 

[EDA notebook](2_data_wrangling_3_eda.ipynb)

* The star-rating distributions all checked out to be normal. It is very common with explicit ratings to see a diminished number of low ratings.

![](./6_README_files/star_counts.png)

# 4. Preprocessing and training

[Preprocessing notebook](4_preprocess_train_5_modeling.ipynb)

# 5. Algorithms & Machine Learning

[Modeling notebook](4_preprocess_train_5_modeling.ipynb)

I chose to work with the Python [surprise library scikit](http://surpriselib.com/) for training my recommendation system. I tested all four different filtered datasets on the 11 different algorithms provided, and every time the Single Value Decomposition++ (SVD++) algorithm performed the best. It should be noted that this algorithm, although the most accurate is also the most computationally expensive, and that should be taken into account if this were to go into production.

![](./6_README_files/algo.png)

>***NOTE:** I choose RMSE as the accuracy metric over mean absolute error(MAE) because the errors are squared before they are averaged which gives the RMSE a higher weight to large errors. Thus, the RMSE is useful when large errors are undesirable. The smaller the RMSE, the more accurate the prediction because the RMSE takes the square root of the residual errors of the line of best fit.*

**WINNER: SVD++ Algorithm**

This algorithm is an improved version of the SVD algorithm that Simon Funk popularized in the million dollar Netflix competition that also takes into account implicit ratings (*yj*). Using stochastic gradient descent (SGD), parameters are learned using the regularized squared error objective.

![](./6_README_files/forumla.png)

# 6. Conclusions

[More details about this process...](https://colab.research.google.com/drive/1kAlvwwJnGcdCAJD8oFokT3gtJF2UnyZP)

After choosing the SVD++ algorithm, I tested the accuracy of all four different filtered datasets. The dataset which filtered out any route names occurring less than 6 times performed the most accurate predictions. Thus, it was chosen to be the dataset I trained on.

>* All of the dataframes displayed discrepancies with the 1 star ratings(This is to be expected due to the inherent skewed positive ratings). Also, the one star ratings are not imperative to this project's goal. It is more important that the 1 star ratings are different enough to be filtered out of the top ten routes recommended to users. 
>* Notice the 3-star rating has a fat bulge at the top of the "violin" which indicates its predicting 3-star ratings for some of the true 3-star routes. This was not as prominent in the other dataframes
>* The 1-star rating also has a fatter tail than the other datasets displayed

![](./6_README_files/accuracy.png)

# 7. Recommendations
[More details about this process...](https://colab.research.google.com/drive/1kAlvwwJnGcdCAJD8oFokT3gtJF2UnyZP)

**Coldstart Threshold**: There is a problem when only using collaborative based filtering: *what to recommend to new users with very little or no prior data?* Remember, we already set our cold start threshold for the routes by choosing the dataset that filtered out any route occurring less than 6 times. Now, let investigate where to put the threshold for users.

![](./6_README_files/20user_thresh.png)

*It is my hypothesis that the initial filtering of the routes is what affected the RMSE of the users* 

>* Increasing the user threshold to 5 would increase the RMSE by .005 & would lose approximately 40% of the data.
>* Increasing the user threshold to 13 would increase the RMSE by .0075 & would lose approximately 60% of the data
>* If there were a larger increase in the RMSE (>= .01) I would trade my users' data for this improvement. However, these improvements are too minuscule to give up 40%-60% of my data to train on. Instead, I voted to keep some of these outliers to help the model train, and will focus on fine tuning my parameters using gridsearch to improve the RMSE

## 7. Considerations and concerns

[Final Predictions Notebook](https://colab.research.google.com/drive/1vLkoW_4SYessy_igmJxlVz_jEPlgJ06v)

In the final predictions notebook, the user can enter their user_id number and receive a list of top ten routes recommended to them:

![](./6_README_files/predictions.png)

## 8. Future research

* In the future, I would love to spend more time creating a filtering system, wherein a climber could filter out the type, difficulty of climb, & country before receiving their top ten recommendation

* This recommendation system could also be improved by connecting to the 8a.nu website so that the user could input their actual online ID instead of just their user_id number 

* Due to RAM constraints on google colab, I had to train a 65% sample of the original 6x dataset. Without resource limitations, I would love to train on the full dataset. Preliminary tests showed that the bigger the training size, the lower the RMSE. One test showed an increase in sample size could increase the RMSE by .03 (in contrast to the .005 improvement I received when increasing the coldstart threshold)

## 9. Credits

Image by Priscilla Du Pree found on Unsplash.com.

Special thanks to Silvia Seceleanu for her guidance and support and Springboard for curriculumn and project design.

[^1]:  Daniela Coppola, publisher.  “E-commerce as percentage of total retail sales worldwide from 2015 to 2027.”  www.statista.com/statistics/534123/e-commerce-share-of-retail-sales-worldwide/#statisticContainer .  Published Aug 29, 2023.  Accessed Sept 18, 2023.
