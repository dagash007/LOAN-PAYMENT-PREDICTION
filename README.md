# LOAN-PAYMENT-PREDICTION

This is a model that helps to predict whether or not a person will pay back their loan based on historical data, Tensor flow with keras API was used to develop the model.

EXPLORATORY DATA ANALYSIS

•	Used the Pandas info to do a quick exploration of the data which revealed that there are missing values in the data.

•	Performed a seaborn count plot to know how many loans were fully paid and charged off on our historical data.

![](Images/image1.png)

•	Used seaborn’s distribution plot (kind = histogram) to graphically summarize the loan amount.

![](Images/image2.png)
  
•	Used the correlation method to explore the correlation between the continuous numerical features, which showed that the most correlated are the loan amount and the installment payment.

![](Images/image3.png)
 
•	Explored more on the two most correlated features with a scatter plot. To check out if both are not a duplication of the other.

![](Images/image4.png)
 
•	Used a box plot to show the relationship between loan status and loan amount. Although both are quite similar, the plot still showed that that charged off loans are slightly higher than fully paid loans, which means that when the loan amount is slightly higher, there is a probability of the loan not being paid.

![](Images/image5.png)
 
•	Performed further statistical summary on loan status and loan amount, by using a group by on the loan status and a describe method on the loan amount which showed that the mean and standard variation of charged off loans are higher than fully paid loans.

•	Explored the grade and subgrade features and realized the subgrade is a more detailed feature based on the grade.



•	Used a count plot to view the relationship between each grade and their loan status e.g., does grade A have more charge off than paid loan etc.

![](Images/image6.png)
 
•	Performed a count plot on the sub grades and loan status which showed that as we move along the grades from A1-G5, the charge off seem to go higher.

![](Images/image7.png)

•	The previous count plot does not show F and G in full detail, so I extracted the F and G subgrades only and did a count plot with loan status as its hue to show the subgrades F and G in full detail. Seems like the G subgrades hardly pay their loans.

![](Images/image8.png)
 
•	Created a numeric feature ‘loan_repaid’ for ‘loan_status’, with 0 and 1 representing charged off and fully paid respectively.

•	Visualized the correlation between the new feature loan repaid and other numeric features, this showed that interest rate has the highest negative correlation which makes sense since the higher the interest rate the higher the chances of not paying the loan.

![](Images/image9.png)
   
**DATA PREPROCESSING**

•	Used the isnull and sum method to view the summation of null values in each column.

•	Calculated the percentage of each columns null values to decide the null values / columns to be dropped or the ones to be retained. Emp_title(% 5.78), emp_length (% 4.62), title (% 0.44), revol_util (% 0.069), mort_acct (% 9.54) and pub_rec_bankruptcies (% 0.135).

•	Started examining emp_title & emp_length to decide if they are to be dropped or retained.

•	The emp_title has too many unique value data of over 170,000 which is simply unrealistic to be converted to dummy variables, so it has to be dropped.

•	Did a count plot on the unique values in the emp_length feature which showed that most loaners were in the category of 10+ years.

![](Images/image10.png)
 
•	Added the loan status as a hue to display how each category of loaners years of working relates to the charged off and fully paid.
 
![](Images/image11.png)

•	The graph above is not giving out a more detailed information we want, so we try calculating and using a bar chat to plot the percentage of charge offs per category, which showed that people who have worked 10 years and above have a slightly lower charged off rate percentage.

![](Images/image12.png)
 
•	Explored the title and purpose column and realized they are both duplicates of one another, so I dropped the title column.

•	Using the value counts method on mort_acc shows that about %10 of mort_acc feature is null.

•	Decided to fill in the missing data in mort_acc with the average of the feature that is closely related to it, which was total_acc. Created a series total_acc_avg, method fill_mort_acc and used the apply method to fill in the missing values.

![](Images/image13.png)
 
•	 Used the select_dtypes method to view all non-numeric columns in order to either delete or convert to dummy variables using one hot encoding.

•	Converted the string binary values of term variables to integers.

•	I dropped the grade variable since the sub grade variable is a more detailed form of the grade variable.

•	Converted the sub grade variable to dummy variables which was now concatenated with the main data frame.

•	Used one hot encoding to convert the remaining categorical or binary variables ('verification_status','application_type','initial_list_status','purpose').

•	Explored the home ownership variable and realized some categories were too small and had to be incorporated into another category e.g., ANY and NONE category were added to OTHER category.

•	Converted the remaining categories (MORTGAGE , RENT, OWN, OTHER) in the home ownership variable to dummy variables.

•	Explored the address column and realized the zip code could be extracted.

•	After extracting the zip-code, I performed one hot encoding on the new zip-code feature.

•	I went ahead and dropped the issue date due to the feature not having much relevance. Since we are predicting whether the loan will be paid or not, realistically, the loan issue date will not be available.
