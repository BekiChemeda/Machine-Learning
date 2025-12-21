This topic is all about Linear Regression, a fundamental algorithm in machine learning used for predicting a continuous target variable based on one or more input features. Linear Regression assumes a linear relationship between the input variables (features) and the output variable (target).

In this topic, I have implemented a simple Linear Regression model from scratch using Python and currently, I am working on Multiple Linear Regression, which involves multiple input features.

Let me explain some key concepts related to Linear Regression so that it won't be new for you when you explore the codes. I also recommend you to watch below videos before diving into the code implementation. (you can use the whole explanations below as a note or revision only if you have already watched the videos, because almost all the explanations are taken from the videos and rephrased here for better understanding).
Recommended Videos
- [StatQuest: Linear Regression](https://www.youtube.com/watch?v=7ArmBVF2dCs)
- [numiqo: Multiple Linear Regression: An Easy and Clear Beginner’s Guide](https://www.youtube.com/watch?v=i3IadpjctWg)
## Simple Linear Regression vs Multiple Linear Regression

The difference between Simple Linear Regression and Multiple Linear Regression is that Simple Linear Regression uses one independent variable to predict the dependent variable. You can take [Salary Predictor](https://github.com/BekiChemeda/Machine-Learning/tree/main/LinearRegression/Salary-Prediction) Project as an example of Simple Linear Regression which predicts the salary based on years of experience only. which means it has only one feature.

On the other hand, Multiple Linear Regression uses two or more independent variables to predict the dependent variable. For example, predicting house prices based on features like size, number of bedrooms, location, etc. In this case, there are multiple features involved in making the prediction.

The other difference is that Simple Linear Regression can be visualized with a straight line on a 2D graph, while Multiple Linear Regression requires higher-dimensional space for visualization due to multiple features.

The other thing is that there are some assumptions that need to be met for both types of Linear Regression. These assumptions are:
1. Linear relationship: There should be a linear relationship between the independent and dependent variables.
2. Independence: The residuals (errors) should be independent of each other. which means that the value of one observation should not influence or be influenced by another observation.
3. Homoscedasticity: The residuals should have constant variance at every level of the independent variables. which means that the spread of the residuals should be consistent across all levels of the independent variables.
4. Normality: The residuals should be approximately normally distributed.
5. No multicollinearity (for Multiple Linear Regression): The independent variables should not be too highly correlated with each other. which means that no independent variable should be a perfect linear function of one or more other independent variables. for example, if you have two features like "age" and "years of experience," they should not be perfectly correlated. We can check for multicollinearity by taking one independent variable as a function of another independent variable and calculating the R-squared value. If the R-squared value is high (close to 1), it indicates multicollinearity. using the r-squared value we can also check the tolerance and Variance Inflation Factor (VIF) to detect multicollinearity. A low tolerance value (below 0.1) or a high VIF value (above 10) indicates multicollinearity among the independent variables. formula for tolerance is 1 - R² and for VIF is 1 / tolerance. If we detect multicollinearity, we can address it by removing one of the correlated independent variables or by combining them into a single variable either through averaging or creating an index.

## What if we have a feature which is categorical?

Let's say we have a feature like "gender" with categories "male" and "female". We cannot directly use this categorical feature in Linear Regression because the algorithm requires numerical input not alphabetical like "male" or "female". So, we need to convert these categories into numerical values. To make this conversion, we label one category as 0 and the other as 1. For example, we can label "male" as 1 and "female" as 0. This way, the Linear Regression model can interpret the categorical feature as numerical values and use it in the prediction process. To see how it handles using formula look at this formula:
Salary = b0 + b1*(YearsExperience) + b2*(Gender)
Where
- Salary is the dependent variable (target).
- b0 is the intercept (constant term).
- b1 is the coefficient for YearsExperience (independent variable).
- b2 is the coefficient for Gender (independent variable, where Gender is coded as 0 for female and 1 for male).
- YearsExperience is the number of years of experience (independent variable).
- Gender is the categorical variable converted to numerical values.
By doing this, when we calculate the salary, we use 1 for male and 0 for female in the formula which makes it possible for the Linear Regression model to include the effect of gender on salary prediction.


If there is a feature with more than two categories, for example, "education level" with categories like "high school," "bachelor's," and "master's", we can use dummy variables (also known as one-hot encoding) to represent these categories. In this case, we create separate binary variables for each category. For example look at below table:
| Education Level | High_School | Bachelors | Masters |
|-----------------|-------------|-----------|---------|
| High School     |      1      |     0     |    0    |
| Bachelor's      |      0      |     1     |    0    |
| Master's        |      0      |     0     |    1    |
In this example, we create three dummy variables: High_School, Bachelors, and Masters. Each variable takes the value of 1 if the education level corresponds to that category and 0 otherwise. When using dummy variables in Linear Regression, we typically exclude one category to avoid the "dummy variable trap," which can lead to multicollinearity(guess how it leads to multicollinearity). For instance, if we exclude "High School," the regression equation would look like this:
Salary = b0 + b1*(YearsExperience) + b2*(Bachelors) + b3*(Masters)
Where
- Salary is the dependent variable (target).
- b0 is the intercept (constant term).
- b1 is the coefficient for YearsExperience (independent variable).
- b2 is the coefficient for Bachelors (independent variable).
- b3 is the coefficient for Masters (independent variable).
- YearsExperience is the number of years of experience (independent variable).
- Bachelors is the dummy variable for Bachelor's degree (1 if the employee has a Bachelor's degree, 0 otherwise).
- Masters is the dummy variable for Master's degree (1 if the employee has a Master's degree, 0 otherwise).
- High_School is excluded to serve as the reference category. 

The way it leads to multicollinearity is that if we know the values of Bachelors and Masters, we can perfectly predict the value of High_School. For example, if both Bachelors and Masters are 0, then High_School must be 1. This perfect linear relationship among the dummy variables creates multicollinearity, which can distort the regression results. By excluding one category, we avoid this issue and ensure that the model can accurately estimate the effects of the included categories on the dependent variable. 
