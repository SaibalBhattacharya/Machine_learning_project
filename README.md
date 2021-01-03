# Machine_learning_project
Predict user location from login data and test if differences in mean login times are statistically significant

EXECUTIVE SUMMARY

PROJECT:
User login data was donated by a pipeline company which wanted to know if the user location can be predicted with machine learning (ML) models. 

OBJECTIVE:
Use login data to predict user location using different machine learning (ML) algorithms. Also, use NULL hypothesis testing to conclude if differences in mean login times between LA and TX 

INITIAL DATA REVIEW:

	- identify unique users, missing values (login times)
	- extract hour, day, weekday/weekend from login time
	- lump user locations and job titles to reduce data imbalance (during testing and training)
	- identify data outliers and remove them

INITIAL DATA PLOTTING:

	- most logins occur between 5 AM and 6 PM with session times varying between 1 to < 100 minutes 
	- users from TX_all (location) dominate longer session times
	- fewer login sessions occur during weekends, and are normally shorter 
	- whether it be weekday or weekend, longer login times come from TX_all
	- longer session times are fewer on Saturdays and Sundays
	- shorter and fewer login session times come from users working for pipeline section  
	- in comparison to other sections (except pipeline), users from IT section have fewer long session times
	- users from pipeline section normally login between 6 AM and 3 PM  
	- users from IT section normally login between 5 AM and 5 PM
	- users from other departments login anytime between zero and 24 hrs
	- users from all sections (groupname_bin) login both during weekend and weekday

KNN ANALYSIS - RESULTS:

	- KNN (3 trees & including user’s section) – 76% accuracy in predicting user location 
	- KNN (3 trees & excluding user’s section) - 76% accuracy in predicting user location
	- KNN (5 trees & including user’s section) – 75% accuracy in predicting user location

DECISION TREES – RESULTS:

	- Random forest model (5 trees) – 69.8% accuracy in predicting user location
	- Random forest model (40 trees) – 70.8% accuracy in predicting user location
	- Random forest model (100 trees) – 71.1% accuracy in predicting user location
		- Variable importance plot shows that weekend_num (i.e., if user logged in during weekdays or weekend) had the least effect in determining the user’s location

NULL HYPOTHESIS TESTING OF MEAN LOGIN TIMES - RESULTS:

Did the difference in mean login times between users based in TX and LA happen by chance?
	- Mean login time for users based in LA = 24.32 mins
	- Mean login time for users based in TX = 30.1 mins
	- Welch Two Sample t-test:
		- t-value = -18.6, i.e., the difference in means is ~18 times larger than would be expected 		by chance 
		- How often would a result this big happen if the null hypothesis were actually true?
			- Because, p < 2.2e-16; i.e., at least 2.2*10-14 % of the time
			- This is sufficient to reject the NULL hypothesis. Thus, the difference in means of session times between TX and LA users didn’t happen by chance.
Cohen’s d-test:
	- d-estimate = -0.26 (tells us that the sample effect size is small)
	- 95% confident that the true effect size is somewhere between small and very small
