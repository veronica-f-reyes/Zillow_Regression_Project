# README for  Zillow Regression Project
# -------------------------------------

GOALS:
-----
- Predict the values of single unit properties based on transaction data from May 1, 2017 through August 31, 2017.
- Identify the county & state where the properties are located in addition to the distribution of property tax rates

PLANNING:
---------
PLAN -> Acquire -> Prepare -> Explore -> Model & Evaluate -> Deliver

Working through the data science pipeline, we will acquire data using an acquire.py file which pulls data from the Zillow database using SQL and joins 2 tables.
We will prepare the data using a prepare.py file which will get rid of unneeded columns, encode string values to 0s and 1s and create dummies.
Then we will explore the data by looking for possible relationships between features and look at how they are distribute by creating plots and looking at the data.
Next we will create models using . We will then compare the models that were run on training data to validate data before running our model on the test data to get the .  We will then present the findings in a verbal presentation using slides.  

DATA DICTIONARY:
----------------

|Target|Datatype|Definition|
|:-------|:--------|:----------|
| taxvaluedollarcnt                  | 7043 non-null: object| value of the property in dollars  |              |

|Feature|Datatype|Definition|
|:-------|:--------|:----------|
| bedroomcnt            | 7043 non-null: object| number of bedrooms |              |
| bathroomcnt                 | 7043 non-null: object| number of bathrooms  |              |
| calculatedfinishedsquarefeet      | 7043 non-null: int64 | square footage of the building  |              |            |
| taxamount            | 7043 non-null: object| amount of taxes owed  |              ||              |
| fips                   | 7043 non-null: int64|unique ID for location of county   |              |


| phone_service            | 7043 non-null: object | Type of phone service plan a customer has|              |
| multiple_lines           | 7043 non-null: object |indicates whether customer has multiple lines - yes or no|              |
| internet_service_type_id | 7043 non-null: int64|type of internet service customer has -  1 for DSL, 2 for Fiber Optic, 3 for None   |              |
| online_security          | 7043 non-null: object|indicates whether customer has online security - yes, no or no internet service  |              |
| online_backup            | 7043 non-null: object |indicates whether customer has an online backup -  yes, no, or no internet service  |              |
| device_protection        | 7043 non-null: object|indicates whether customer has device protection - yes, no, or no internet service  |              |
| tech_support             | 7043 non-null: object|indicates whether customer has tech support - yes, no, or no internet service  |              |
| streaming_tv             | 7043 non-null: object| |indicates whether customer has streaming tv - yes, no, or no internet service  |              |
| streaming_movies         | 7043 non-null: object| |indicates whether customer has device protection - yes, no, or no internet service  |              |
| contract_type_id         | 7043 non-null: int64| contract term of the customer  - month-to-month, one year, wo year)   |              |
| paperless_billing        | 7043 non-null: object|indicates whether customer has paperless billing - yes or no  |              |
| payment_type_id          | 7043 non-null: int64| customer payment method - 1 for electronic check, 2 for mailed check, 3 for automatic bank transfer, 4 for automatic credit card payment   |              |
| monthly_charges          | 7043 non-null: float64| amount charged to customer monthly  |              |
| total_charges            | 7043 non-null: object| Total amount customer has paid  |              |
***


KEY FINDINGS & TAKEAWAYS:
-------------------------



HOW TO RECREATE THIS PROJECT:
----------------------------

To recreate this project you will need the following files from this repository:
- README.md
- acquire.py
- prepare.py
- explore.py
- Final_Notebook.ipynb

You will also need your own env file with your data base credentials to connect to the SQL database containing Zillow data 

Instructions:
- Read the README.md
- Download the aquire.py, prepare.py, explore.py and Final_Notebook.ipynb files into your working directory, or clone this repository
- Add your own env file to your directory (user, password, host)  
- Run the Final_Notebook.ipynb 


DATA SCIENCE PIPELINE:
----------------------

PLAN:
-----

Project Planning

Goal: leave this section with (at least the outline of) a plan for the project documented in your README.md file.

Think about the following in this stage:

Brainstorming ideas and form hypotheses related to how variables might impact or relate to each other, both within independent variables and between the independent variables and dependent variable.

Document any ideas for new features you may have while first looking at the existing variables and the project goals ahead of you.

Think about what things in your project are nice to have, versus which things are need to have. For example, you might document that you will only worry about trying to scale your features after creating and evaluating a baseline model.


ACQUIRE:
--------
    Call the acquire.py file to run the functions to obtain Zillow data using a SQL query from the Codeup Data Science Database: zillow
    It returns a pandas dataframe.  The SQL query joins two tables and filters on single family properties that were listed between May 1, 2017 to August 31, 2017.
    The data is filtering to return single unit properties defined within the propertylandusetypeid of codes: 261- Single Family Residential, 262 - Rural Residence, 
    263 - Mobile Home, 264 - Townhouse, 265 - Cluster Home, 266 - Condominium, and 279 - Inferred Single Family Residential.   

    The SQL query that is run is shown below:
                '''
                 SELECT bedroomcnt, bathroomcnt, calculatedfinishedsquarefeet, taxvaluedollarcnt, yearbuilt, taxamount, fips
                FROM properties_2017
                JOIN predictions_2017 USING (id)
                WHERE propertylandusetypeid IN ('261','262','263','264','265','266','279') 
                AND transactiondate BETWEEN '2017-05-01' AND '2017-08-31'
                '''


PREPARE:
--------
Prep

Goal: leave this section with a dataset that is split into train, validate, and test ready to be analyzed. Make sure data types are appropriate and missing values have been addressed, as have any data integrity issues.

Think about the following in this stage:

This might include plotting the distributions of individual variables and using those plots to identify and decide how best to handle any outliers.

You might also identify unit measures to decide how best to scale any numeric data as you see necessary.

Identify erroneous or invalid data that may exist in your dataframe.

Add a data dictionary in your notebook at this point that defines all the fields used in your model and your analysis and answers the question, "Why did you use the fields you used?". e.g. "Why did you use bedroom_field1 over bedroom_field2?", not, "Why did you use number of bedrooms?"

Create a prep.pyfile as the reproducible component that handles missing values, fixes data integrity issues, changes data types, scales data, etc.

EXPLORE:
--------

Goal: I recommend following the exploration approach of univariate, bivariate, multivariate discussed in class. In that method, you can address each of the questions you posed in your planning and brainstorming and any others you have come up with along the way through visual exploration and statistical analysis. The findings from your analysis should provide you with answers to the specific questions your customer asked that will be used in your final report as well as information to move forward toward building a model.

Think about the following in this stage:

Run at least 1 t-test and 1 correlation test (but as many as you need!)

Visualize all combinations of variables in some way(s).

What independent variables are correlated with the dependent?

Which independent variables are correlated with other independent variables?

Make sure to summarize your takeaways and conclusions. That is, the Zillow data science team doesn't want to see just a bunch of dataframes, numbers, and charts without any explanation; you should explain in the notebook what these mean, interpret them.

In exploration, you should perform your analysis including the use of at least two statistical tests along with visualizations documenting hypotheses and takeaways.

MODEL:
------

Modeling

Goal: develop a regression model that performs better than a baseline.

Think about the following in this stage:

Extablishing and evaluating a baseline model and showing how the model you end up with performs better.

Documenting various algorithms and/or hyperparameters you tried along with the evaluation code and results in your notebook before settling on the best algorithm.

Evaluating your model using the standard techniques: plotting the residuals, computing the evaluation metrics (SSE, RMSE, and/or MSE), comparing to baseline, plotting 
y
 by 
^
y
.

For some additional options see sklearn's linear models and sklearn's page on supervised learning.

After developing a baseline model, you could do some feature engineering and answer questions like:

Which features should be included in your model?

Are there new features you could create based on existing features that might be helpful?

Are there any features that aren't adding much value?

Here you could also use automated feature selection techniques to determine which features to put into your model.

In modeling, you should establish a baseline that you attempt to beat with various algorithms and/or hyperparameters. Evaluate your model by computing the metrics and comparing.

DELIVER:
-------

- Present a report in the form of verbally supported slides.

    The report/presentation slides should summarize your findings about the drivers of the single unit property values. This will come from the analysis you do during the exploration phase of the pipeline. In the report, you should have visualizations that support your main points.


- A github repository containing your work with any .py files required to acquire and prepare the data and a clearly labeled final Jupyter Notebook that walks through the pipeline.








