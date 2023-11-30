# AI & Machine Learning Project
### Dataset: Trains

### Members
- Ayham Alroumi 289941
- Janhvi Goje 286971
- Davoud Danish 289951

# Introduction
In this project, we take on the role of the a **Senior Data Analyst** at ThomasTrain company and our goal is to analyse customer satisfaction in the company which would ultimately help the marketing team in increasing customer retention through targeted promotions. We are provided the “trains_dataset.csv” dataset to use for our analysis which provides a comprehensive set of features that encompass customer demographics, service ratings, travel-related information, and more. These features serve as valuable inputs for analyzing and predicting customer satisfaction.

# Methods

In order to access the jupyter notebook, containing the background code used for this analysis, you need to follow the following steps:
- Save the 'environment.yml' file (uploaded in this repository).
- Open the terminal or command prompt.
- Run: conda env create -f environment.yml
- Run: conda activate ai_project_env
- Run: jupyter notebook

Now, you are ready to access the project. 

Our project approaches data analysis of the trains.csv dataset with the intention of drawing insights regarding customer satisfaction. In order to do this we first need to understand our dataset through and through, with visualisation and statistical operations (built-in within python). The flow of the project is as follows:

<img width="882" alt="Screenshot 2023-11-29 at 4 51 54 PM" src="https://github.com/janhvigo/289941/assets/149782498/07d179d4-afbb-4c7b-8b77-cd6ff44e6e95">

# Experimental Design

First, we noticed how most of the columns in the dataset were ratings which was hard to analyse as the ratings, individually, don't hold much value as much as they do on average. This is especially true when we are dealing with customer satisfaction as a customer who gave very less rating on one factor but pretty high rating overall is said to "satisfied". Therefore, we decided to add the 'Average_rating' column to quantify the ratings better as a continuous variable. This new column is a better judge of a customer's satisafaction than all the ratings individually.

We then started with exploring the dataset and found that the categorical variables existed. Initially, we thought of dealing with categorical variables and continuous variables separately and decided to conduct separate analysis on each of them. However, it was realised that the Correlation Heatmap was an extremely informative visualisation which helped us gain much insight into the dataset. Therefore, we decided to encode the categorical variables early on in the project instead of just before modelling. This enables us to include the categorical variables in the correlation map which indeed was very insightful.

We also noticed that there were two outliers- rating approximately 1 and "satisfied". This, logically, doeesn't make any sense because it means that there were no ratings that were more than one but, for some reason, the customer is satified. This might be a misreading or a factor which made these two customers 'satisfied' was not included in the rating section. However, we don't have enough data to explore this anamoly so we choose to remove these two data entries.

Further expanding on the correlation maps, there were a few variables which had the correlation of less that |0.15|. We initially decided to keep these variables for the sake of maximal accuracy, however, we noticed that this greatly slowed down the GridSearch Process used later in the project (the program kept running overnight!). Therefore, we decided to remove the columns that had little to no significance on 'Satisfied' column which was our key variable.

# Results

### Main Findings

First, we made a Bar Graph with the columns Gender, Work or Leisure, Ticket Class and Loyalty and we gained some insights on consumer behaviour, some were obvious while some were not so obvious. First, it was obvious that there are more 'Loyal' customers who answered the survey and most of them are satified. This is because Loyal customers are in fact loyal because they are satified with the services. The high number of responses can be interpreted as people who are Loyal are more likely to pay attention to a survey conducted by the organisations as compared to Disloyal customers. Gender ratings were fairly balanced as train services are not different for men and women.

An interesting observation was that people who travelled for work were way more satisfied than those who travelled for leisure. We know that people travelling for work prioritise efficiency over luxury which might mean that the efficiency aspects of the company (schedules and on-time arrival) are well but the overall consumer experience might not be 'fun', something that's desired by leisure travellers. We also noticed that Premium class members are way more satisfied than Economy or Smart class members which means that the company should improvise vervices in these areas.

The density plots give us a visual understanding of the distribution of four different continuous variables from your dataset.

Density Plot of Age:

The distribution of age appears to be bimodal, with two peaks suggesting there are two age groups that are most common in this dataset.
The plot indicates a slight right-skewness, meaning there are more younger individuals than older ones, but there is a significant presence of middle-aged to older individuals as well.

Density Plot of Arrival Delay in Minutes and Density Plot of Departure Delay in Minutes:

Both arrival and departure delay plots show a highly right-skewed distribution, indicating that most of the train arrivals and departures are close to on-time, with fewer instances of longer delays.
The sharp peak at the lower end of the scale suggests that delays are generally short.
The long tail to the right suggests that while most delays are short, there are a few cases with very long delays.

Density Plot of Average Rating:

The average rating distribution appears to be left-skewed, indicating that most ratings are high, with a peak around 4 out of 5.
The plot suggests that there are few very low ratings and most customers tend to give a rating above the midpoint of the scale.

From these plots, we can deduce that:

- Most passengers are either in the younger or middle-aged bracket, with fewer older passengers.
- Delays (both arrival and departure) are typically short, but there are outlier cases where the delays can be quite long.
- Customers generally seem to be satisfied with the service, as indicated by the higher average ratings.

These insights could be valuable for the train service provider, indicating areas where service is performing well (high average ratings) and aspects that might require attention (the occurrence of long delays, even if infrequent).

Density Plot of Distance:

The plot shows a distribution with multiple peaks, which suggests that there are several common distances at which people travel. It could indicate regular routes or distances that are more popular or available for traveling.There's a significant peak at the lower end of the distance range, indicating that a large number of trips are short-distance. Following this, there are smaller peaks, which could represent less frequent but still common travel distances. The long tail to the right indicates that there are fewer instances of long-distance travel, but such trips still occur.

After preprocessing the data, we notice that in our Scatter Plot, there are no outliers (because we removed them) and the correlation heatmap has way less insignifant variables that taint the graph dark blue.

We tested three models: Logistic Regression, Decision Trees and Random Forests. with the following results:

<img width="448" alt="Screenshot 2023-11-29 at 5 43 49 PM" src="https://github.com/janhvigo/289941/assets/149782498/c642ad46-fcad-4f36-bc8d-29bc3f858657">

**Choosing the Right Metric**
Let's go back to our purpose with this project. Our goal is to give interpretations that will ultimately help the marketing team in understanding the customers’ satisfaction to **effectively target users** with promotions and making the **retention higher**. Therefore, our focus with our model remains minimising false negatives (classifying unsatisfied customers as satisfied). We don't really care much about false positives (classifying satisfied customers as unsatisfied) because at worst, we give them more incentives to purchase which would do no harm, especially when higher retention is one of our purposes. 

Therefore, the right metric to focus on is **Recall**

**Choosing the Best Model**
Considering Recall as our most important metric, we should choose the model with the highest recall, i.e. **Random Forests** (0.93). Random Forest is also ideal in terms of every other score with the highest accuracy (0.95), precision (0.96) as well as the F1 score (0.94).

# Conclusion

In conclusion, we notice that for all the metrics, including Recall, our model of Random Forests performs really well on the test set we formerly initialised with excellent scores of above 0.9. Therefore, we can conclude that our model is a good model.

Although this project explores the analysis of customer satisafaction with enough rigour, it ignores any improvements that was made by the company over time as we drop the Date and Time column, deeming it as unimportant. An area of further study could be taking into consideration the Date and Time column and performing a time series analysis to gain more specific insights into consumer behaviour. This analysis would be highly insightful as it could help up understand if there were certain aspects of the services that were improved as the time passes (seen through improved ratings). Through this, the company can direct its focus more on improving the aspects of the services that still receive a lower rating rather than making a general inference based on the average rating. 
