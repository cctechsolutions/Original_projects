# Big Mountain Ski Resort
## Using random forest modeling to maximize business profits

![image](https://github.com/cctechsolutions/Original_projects/blob/main/revenue_analysis/additional_files/images/1bhmh2MHxcSbMdDqYW7C1jtGN7C8F-eaZ68cTuIR-i1Yhl-R2bA.png)

*Random forest regression is a powerful machine-learning algorithm that analyzes complex datasets and accurately predicts continuous values.  This predictive model can provide invaluable insights to guide businesses in decision-making.  In this project, various predictive models are created and compared to guide a fictitious ski resort in setting the ideal ticket price to maximize profits.*

# Method

1. **Project proposal:**  Suggested plan for research methods and objectives

2. **Data wrangling:**  Found, imported, cleaned, and transformed data to prepare for analysis

3. **Exploratory data analysis:**  Examined the dataset to find patterns and insights and created graphics to visualize the data

4. **Develop machine learning algorithms:**  Created, evaluated, compared, fine-tuned, and improved models to determine which was best in this context

5. **Modeling:**  Used the chosen model to predict which business decisions will best serve the company and maximize profit
   
6. **Conclusions and recommendations:**  Examined the results and recommended future business actions

 &nbsp;   
***Final model:   Random Forest Regression***
     
The algorithm that performed best for determining what ticket price is best for the resort was a random forest regression model.  One of the reasons for choosing this model is that the random forest regression had a smaller mean absolute error than using the mean or the linear regression model.  The random forest model also provided more detailed business insights, such as which features of the resort had the largest impact on business outcomes.
      
# 1. Background
[Problem identification](./01_problem_identification.pdf)

Big Mountain Resort offers access to 105 trails and spectacular views of Glacier National Park and Flathead National Forest and hosts about 350,000 visitors each year. The resort has remarkable facilities, including a newly installed additional chair lift.  

Using data from the resort and its competitors, we can identify opportunities for the resort to make the most of its current facilities, set the best possible ticket prices, ensure that new investments pay off, and plan for the most profitable future.
      
## About the data:
The dataset used for this project is for practice purposes and contains partly fictional data.  Provided by Springboard curriculum, this information was contained in a single CSV file with about 330 observations.  For each resort, the dataset contains data about the following variables:

#### *Resort information*
* Name: name of the resort   
* Region: the region that contains the resort (divided primarily the same as state divisions, though with some exceptions)   
* state: the state in which the resort resides
#### *Resort features*
* summit_elev: elevation above sea level at the summit of ski slopes (in feet)
* vertical_drop: difference in elevation over the distance of ski slope (in feet)
* base_elev: elevation above sea level at the base of ski slopes (in feet)
* trams: number of trams for transporting visitors
* fastEight: number of eight-person detachable chairlifts
* fastSix: number of six-person detachable chairlifts
* fastQuads: number of four-person detachable chairlifts
* quad: number of four-person chairlifts
* triple: number of three-person chairlifts
* double: number of two-person chairlifts
* surface: number of surface lifts
* total_chairs: number of chairs in chair lift(s)
* Runs: number of total ski runs
* TerrainParks: number of terrain or snow parks
* LongestRun_mi: length of the longest ski run (in miles)
#### *Resort logistics*
* daysOpenLastYear: number of days open the previous year
* yearsOpen: number of years the resort has been open total
* averageSnowfall: average amount of snowfall in inches
* SkiableTerrain_ac: number of acres available for skiing
* SnowMaking_ac: number of acres available for making snow
* projectedDaysOpen: the anticipated number of days a resort is likely to be open during the following year
* NightSkiing_ac: number of acres available for skiing after dark
#### *Ticket price information*
* AdultWeekday: price for an adult for one weekday
* AdultWeekend: price for one adult for one weekend day
     
# 2. Data wrangling
[Data wrangling notebook](./02_data_wrangling.ipynb)

Before analysis can begin, the raw data must be examined and cleaned.  Identifying and correcting, fixing, or removing any inaccurate and inconsistent data will ensure that analysis and modeling are as reliable and useful as possible.

* **Problem 1:** Missing values:  13 of the 27 columns contained at least one missing value.  Some of the missing values may represent zeros or categories that do not apply to certain resorts.  For example, when a resort has no fast lifts, these columns may be left blank rather than filled with a zero in each of the columns for types of fast lifts.  However, about 16% of the resorts are missing ticket pricing information.  As one of the ways we might help our resort estimate an ideal ticket price is to compare to prices at similar resorts, this information is very important.  We can logically assume that these missing values would not imply that the ticket price of each resort would be $0.  **Solution:** Rather than make assumptions about the missing prices, which could drastically affect our later recommendations, I dropped rows that contained no information about ticket price.  However, resorts that gave one ticket price, either in the weekend or weekday price category, were retained and could be used for insights and comparisons.

* **Problem 2:** Some values given for categorical variables were in a different format than others.  Some appeared to be added as a joke, such as the values "Absurd" and "YOLO" in the column for relationship status.  **Solution:** For the education variable, I looked for information to learn which of the unknown labels were most equivalent to the education system in the US, as that is what I am most familiar with.  I then replaced the terms, "Basic," "2n cycle," with "High School" and "Master's" so that the format was the same across all observations.  I dropped the rows with "Absurd" and "YOLO" for relationship status as I had no way to determine what the true response should have been, nor was there any average value for that feature that I might use to impute them.

* **Problem 3:** There were more features than we would use for our analysis.  Machine learning algorithms can manage extremely large datasets with many dimensions, but each dimension adds complexity and can increase the time required to train and test models. Solution: While I did drop unnecessary columns such as customer ID number, I wanted to maintain as many features as possible that might prove useful. Therefore, I combined features such as "Kidhome" and "Teenhome" into a single feature for customers with a child or children at home.

# 3. Exploratory analysis
[Exploratory data analysis notebook](./03_exploratory_data_analysis.ipynb)

# 4. Preprocessing and training models
[Preprocessing notebook](./04_preprocessing_and_training.ipynb)

# 5. Predictive modeling
[Modeling notebook](./05_modeling.ipynb)

# 6. Conclusions and recommendations
[Presentation for business leaders](./06_presentation.ipynb)     

[Project Report](./07_project_report.ipynb)
