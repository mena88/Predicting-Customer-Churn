# Predicting Employee Churn

## Table of Contents

- [Description and deliverables](#description-and-deliverables)
- [Project Overview](#project-overview)
- [Data Sources and Description](#data-sources-and-description)
- [Tools Used](#tools-used)
- [Imports](#imports)
- [Initial EDA and data cleaning](#initial-eda-and-data-cleaning)
- [Further EDA and Results](#further-eda-and-results)
- [Model Building](#model-building)
- [Visualizations for Model Building and Assessment](#visualizations-for-model-building-and-assessment)
- [Conclusion and Recommendations](#conclusion-and-recommendations)
- [References](#references)


# Description and deliverables
This was my capstone project for the advanced data analytics course by Google. it gave me the opportunity to analyze a dataset and build predictive models that can provide insights to the Human Resources (HR) department of a large consulting firm.

The deliverables for this project were; 
1. A Pace strategy document/Proposal
2. Executive summary
3. Code notebook
4. Model evaluation results, interpretation and visualizations

### Project Overview

The HR department at Salifort Motors wanted to take some initiatives to improve employee satisfaction levels at the company. They collected data from employees, and wanted to derive insights from the data. So they consultted with our firm as data analytics professionals and asked us to provide data-driven suggestions based on our understanding of the data. They have the following question: what’s likely to make the employee leave the company?
Our goals in this project were to analyze the data collected by the HR department and to build a model that predicts whether or not an employee will leave the company and also find out, if they do leave, what could be responsible for their leaving.
If we are able to predict employees likely to quit, it might be possible to identify factors that contribute to their leaving. Because it is time-consuming and expensive to find, interview, and hire and train new employees, increasing employee retention will be beneficial to the company.

### Data Sources and Description
The data for this activity was from Salifort motors management team
The dataset that was used for this project contained 15,000 rows and 10 columns for the variables listed below. 
**Note:** More information about the data can be found here [Kaggle](https://www.kaggle.com/datasets/mfaisalqureshi/hr-analytics-and-job-prediction?select=HR_comma_sep.csv).

Variable  |Description |
-----|-----|
satisfaction_level|Employee-reported job satisfaction level [0&ndash;1]|
last_evaluation|Score of employee's last performance review [0&ndash;1]|
number_project|Number of projects employee contributes to|
average_monthly_hours|Average number of hours employee worked per month|
time_spend_company|How long the employee has been with the company (years)
Work_accident|Whether or not the employee experienced an accident while at work
left|Whether or not the employee left the company
promotion_last_5years|Whether or not the employee was promoted in the last 5 years
Department|The employee's department
salary|The employee's salary (U.S. dollars)

### Tools Used
  - Jupyter notebook [Download here](https://jupyter.org)
 
### Imports/Packages
The imports packages included:
1.	Pandas 
2.	Numpy 
3.	Matplotlib
4.	Train_test_split 
5.	LogisticRegression, Decision Tree and Random Forest Classifiers
6.	Sklearn.metrics, and OneHotEncoder 
7.	ProfileReport
8.	Pickle
The above imports and packages were used to generate a quick report, preprocess, do EDA, build, visualize, and evaluate the model.

### Initial EDA and data cleaning
Here we tried to:
- Understand our variables
- Clean our dataset (missing data, redundant data, duplicates, outliers)

#### Summary of Initial EDA
From the initail EDA the following can be deduced;
1. The dataset contains 15,000 rows, and 10 columns, nil missing values and about 20% of the dataset are duplicates same was droped.
2. The data set contains the following columns and data types; 

Column Name    |Data Type
-----|-----
satisfaction_level|float64
last_evaluation|float64
number_project|int64
average_montly_hours|int64
time_spend_company|int64
Work_accident|int64
left|int64
promotion_last_5years|int64
Department|object
salary|object

Important to note is that there are object type variables in the data which were converted to numeric data form to allow for more efficient manipulation.

3. The column names were not uniform, same was corrected, all column format made uniform by applying the snake_case format to all the column heads and spelling mistakes were corrected.

4. Outliers in the dataset were identified using a function that applied calculated upper and lower limit values, and the outliers were removed from the resulting variables. This is imprtant as certain models are more sensitive to outliers than others and these outliers may need to be removed depending on our choice of model.

**Boxplot of Tenure Showing Outliers**

![Boxplot to detect outliers in tenure](https://github.com/mena88/Predicting-Customer-Churn/assets/97759151/185e05e1-9e0f-4853-96e1-aec395f33c51)

### Further EDA and Results
1.	Here we examined, the class distribution of our target variable 
2.	Relationship among various variables were explored using various visualizations

### Results of Further EDA
The distribution of the employees that left vs those that stayed was about 17/83, that means of all the employees in the dataset, 17% left the company

#### Next we examine the results of other exploratory analysis

**Comparing Satisfaction Level vs. Average Monthly Hours for Employees who Left and Stayed**

![Avarage Hours Vs Satisfaction for both classes](https://github.com/mena88/Predicting-Customer-Churn/assets/97759151/38ac3133-addb-4e5d-9292-bff70cc7f22e)

From our plot above, we tried to compare average monthly hours and satisfaction level and how these two affected those that left or stayed.
From the plot, we see how average hours worked monthly and satisfaction influenced leaving or staying, even though the plot looked unusual, some deductions could still be made;
Everyone that worked 100hours and below stayed, irrespective of their level of satisfaction, this could be due to the flexibility that working fewer hours offered such employees.
Of those that had the highest level of satisfaction, close to 1, none of them left, although none of them also worked up to 300hours. In essence if employees are very satisfied with the company, they stayed not minding how much work they did.
Those that worked significantly more had the least satisfaction, and all of them left, it is not clear though weather their dissatisfaction was due to them being overworked and burning out or other reasons such as low level of satisfaction with the job or company or poor compensation.
All those who worked 300hours and above left, this may be attributed to them being overworked.
In conclusion, satisfaction level as well as average number hours worked seem to be good indicators of the employees leaving or staying. And finding ways to improve the level of satisfaction and regulating the number of hours worked might be worth investing in.

**Comparing Level of Satisfaction vs Number of Projects for those who Left and Stayed**

![Satisfaction vs Number of projects for both classes](https://github.com/mena88/Predicting-Customer-Churn/assets/97759151/d805993e-483e-411e-a3af-5644107ce304)

From the plot;
1.	The plot also appears strange and there is no pattern or clear correlation between the two.
2.	Everyone that worked on 7 projects left the company, irrespective of their level of satisfaction although none of them had a satisfaction score of up to 0.7
3.	Also, all the least satisfied employees in all project categories left, that’s irrespective of the number of projects worked on.
4.	it could be deduced that, those who worked on more projects, also worked longer hours, and at the end were probably burnout and irrespective of how satisfied they were, they still left.

**Comparing the Satisfaction level  among employee in both classes**

![Comparing satisfaction among the two classes](https://github.com/mena88/Predicting-Customer-Churn/assets/97759151/4a7e944d-133b-4a8c-aa1d-3e87c5698c49)

From the boxplot above;
Those employees that stayed had a higher mean satisfaction score, compared to those who left. This is demonstrated by the table below as well in figures.

Left    |Mean    |Median
-----|-----|-----
No|0.6674|0.691
Yes|0.4405|0.41

Even though there was no linear relationship between satisfaction and both average monthly hours and number of projects worked on, the three factors together contributed significantly to whether a customer would leave or not. So trying to reduce the hours and number of projects employees worked could improve the level of satisfaction and in turn reduce employee churn

**Examining distribution of those that left or stayed by department**

![Stayed vs left by department](https://github.com/mena88/Predicting-Customer-Churn/assets/97759151/4ef32dd4-54e6-4356-bd44-7fc05c12e46c)

From our graph above, the following could be inferred;
1.	Churn was highest in the sales, technical and support departments and least in the management, RandD and accounting departments respectively.
2.	It’s important to note however, that the department with the highest churn also had the highest number of employees. For instances, sales is probably one of the most demanding departments as there are always difficult targets, if this is coupled with low pay and poor motivation, it may drive turnover of employee.
3.	Thus, management may consider ways of improving welfare of sales employees as well as others, there are a lot of ways to achieve this, including percentage compensation at certain thresh holds of product sales.
4.	There were less churn at the level of management, this was expected as it is comprised of the decision making unit of the company and probably the best paid as well.

**Distribution of those who left and stayed by number of projects**

![Stayed vs left by number of projects](https://github.com/mena88/Predicting-Customer-Churn/assets/97759151/3f054671-2100-4822-826a-3e19cc913853)

The plot above compares the count of those that left and stayed by the number of projects they were involved in, and the following deductions can be made;
1. Those that worked around the mean/median number of projects and 1 standard deviation away from this were the least likely to leave.
2. As the number of projects increases to the right and decreases to the left, the number of those who left also increased. An increase to the right(increase in the number of projects), could indicate discontent from the bornout of being involved in too many projects that the employee could possibly handle effectively. While on the other hand as the number of projects decreased to the left we also saw a sharp increases in the number of those that left, here some scenerios come to mind; a. could it be that these category were not given enough tasks because they were new and still trying to familiarize with the company procedures, b. Were they always unable to meet targets resulting in less trust and subsequently a reduction in the number of projects asigned to them. c. Or were they already on their way out of the company?
3. All those that worked on 7 projects all left

**Distribution of those who left and stayed by tenure**

![Stayed vs left by tenure](https://github.com/mena88/Predicting-Customer-Churn/assets/97759151/3d3e7554-86eb-4e2a-adf9-acce7dfa092f)

From our plot above;
1.	It is clear that no employee who has worked for more than 6yrs left the company. This could be explained by a number of factors; a. Loyalty factor, b. Job satisfaction, c. Good renumeration d. Carear progression. This could also represent outliers in our dataset.
2.	A high proportion of those who stayed were from the management department, about 14% compared to sales for instance with only 3% staying past the 6 year mark. Again this likely down to pay as is conformed below
3.	Majority of those who stayed, about 73% belonged to the medium and high salary class, in essence, the higher the salary the higher the likelihood of staying

### Model building
#### The following steps were undertaken to build logistic regression, Decision Tree and Random Forest models;
1.	Plot Correlation heatmap to check for multicollinearity 
2.	Isolated the dependent and independent variables (y and X variables respectively)
3.	Split the data into training and testing sets, using the train_test_split method of sklearn
4.	Instantiated a logistic regression model.
5.	Then fit the model to the training dataset
6.	Predicted customer satisfaction (y) given inflight entertainment(X)
7.	Predicted customer satisfaction given inflight entertainment and other independent variables
8.	Specified model parameters
9.	Considered the assumptions of the various models.  

### Visualizations for Model Building and Assessment 
The following steps were undertaken
1. Plot correlation heatmap
2. Plot Confusion matrix diagram and Feature importance
3. Print out models Accuracy, Precision, Recall, F1 Score and ROC_AUC score
4. Derive insight from the values in 1 and 2 above

1.	Correlation heatmap

   ![correlation heatmap](https://github.com/mena88/Predicting-Customer-Churn/assets/97759151/5dec4e98-916e-4d4a-8f74-c5871e738b5c)

From our heatmap, there were no variables that were highly correlated.
So, we proceeded to build our models, which will predict those that will leave the company and those that will not.

2.	Confusion matrix diagrams

  	Logistic Regression
    ![Confusion matrix diagram](https://github.com/mena88/Predicting-Customer-Churn/assets/97759151/7ee3321a-7860-47fd-8308-4a82ba125095)

    Tree Based Model
    ![Confusion matrix _decision_tree](https://github.com/mena88/Predicting-Customer-Churn/assets/97759151/b9f01da3-2f90-4a5f-bb77-f2194d522b7e)

2b. Feature Importance Diagram 
    ![Random forest feature importance](https://github.com/mena88/Predicting-Customer-Churn/assets/97759151/8741d22d-1b59-4edb-9716-6937b2975763)

3.	Results and Considerations 
Below is a table comparing metrics from the three models

Model    |Accuracy    |Precision    |Recall    |F1_Score    |ROC_AUC|
-----|-----|-----|-----|-----|-----
Logistic Regression|0.8202    |0.4444    |0.2633    |0.3307    |0.5982
Decision Tree_cv|0.9780    |0.9554    |0.9121    |   0.9332|0.9741 
Random Forest_cv|0.9811    |0.9707    |0.9157    |0.9423    |0.9818 

4.	Derive Insight from the Results and diagrams
   
1. The weighted averages of our logistic regression model were good overall with an F1_score of 82%, this model excelled at predicting the employees who would stay, but did poorly at predicting those that would leave which was the reason for the project in the first place.
2. The decision tree model showed significant improvement even before tunning, with even further improvement with cross validation.
3. The random forest model had the best performance of all the models, and thus was the recommended model for prediction
4. The model’s ability to correctly predict those who will leave improved as our models also showed progressive reduction in the number of Type I and II errors made as we moved across the models.

### Conclusion and Recommendations
**Conclusion**
The models and the feature importance extracted from the models confirm that employees at the company are overworked and most of the employees who left were not very satisfied with the company, although it was not clear if their dissatisfaction was from long hours of work or high number of projects as there was no linear relationship between leaving and both variables.

**The following recommendations were presented to the stakeholders to retain employees:**
1. Cap the number of projects that employees can work on. This in turn may reduce the number of hours the employees have to work, reduce burnout and probably improve their job satisfaction since they will now have more time for other important things in their lives.

2. Ensure that loyalty and hard work is rewarded appropriately especially with respect to promotion of deserving employees and review of renumeration as may be required.

3. If employees must work for very long hours beyond the company's established average requirement, the should be compensated appropriately or such long hours of work should be avoided. The task could be spread to involve more employees.

4. If the company does not have an overtime policy it should develop one, if otherwise employees should be properly informed of same. The company should also be clear on the expectations in terms of workload and time off.

5. There should unhindered communication between management and employees at all levels, this can be achieved through regular meetings at all levels.

### References
1. Google Advanced Data Analytics Course Resources
2. Google
3. StackOverflow
4. StackUp
5. ChatGPT
