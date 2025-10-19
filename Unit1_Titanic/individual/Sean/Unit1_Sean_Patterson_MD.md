**Titanic Data Set Executive Summary** 

	The Titanic data set includes a vast amount of observations with demographic and sociological factors of different passengers and whether or not they survived the infamous crash. Predictors include age, ship class, and gender, and a binary target variable of survival (1 or 0). I conducted an exploratory data analysis and trained a model to predict age and use those predictions to impute the missing values. The cabin column had so many missing values that I dropped the entire column. 

	The first influential finding discovered was that there are significant disparities in survival rates by gender. With females surviving the crash at a probability over .7 and males at around .4, this represents a .3 difference in survival rates. This data can be found in the bar graph in the executive summary dashboard.

	The gender differences continued to persist as one of the most relevant factors to survival. Even when looking at the different classes, females always had a higher survival rate than males. Class 3 females had a higher survival rate than Class 1 males. Further looking into class, we can see that passengers in first class had a higher rate than those in second class and third class. Indicating that passenger class is a significant predictor of survival rate.

	Age was the final influential predictor that was identified. From the correlation matrix, we can see that age has a negative correlation with survival. The,n when further visualizing age, we can see that survival decreases every year by age group. 

In conclusion, the Titanic data set offered a large number of predictors for a passenger's survival rate. In the end, three predictors were seen as being the most influential: Gender, Class and Age Group. Females, younger people, and higher-class passengers have the greatest chance of surviving. 

We can infer tha,t as they were evacuating the Titanic, priority was given to women and children and males were made to stay on the boat. In addition, we can infer that those in first class were on a nicer part of the ship and this allowed them to exit more easily onto to lifeboat and survive. 