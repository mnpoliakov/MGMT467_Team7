Orion Barrett-Tzannes  
 Professor Chaturvedi  
 MGMT 467  
 October 19, 2025  
 Unit 1 Assignment Summary

For this assignment I analyzed the Titanic dataset to figure out what affected passenger survival. I started by checking for missing data. Age, Cabin, and Embarked had gaps. I dropped Cabin because too much was missing, removed the two rows missing Embarked, and used a Random Forest model to predict missing Age values instead of deleting them.

After cleaning the data I split it into two parts, one with known ages and one with missing ones, so I could train the model. I used features like Pclass, Sex, SibSp, Parch, Fare, and Embarked to predict Age. Once the model was trained I filled in the missing ages and had a complete dataset to work with.

Next I looked at distributions of Age, Fare, Pclass, and Sex. Fare was skewed which might need a log transformation later. I noticed younger passengers, women, and first-class passengers were more likely to survive.

Finally I checked which variables were most linked to survival. Sex and Pclass were the strongest predictors. Women and first-class passengers had higher survival rates, and younger people also did better, matching the idea of “women and children first.”

