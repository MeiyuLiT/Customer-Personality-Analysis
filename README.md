# Customer Personality Analysis

Nowadays, due to the more and more fierce competition in the market, it is increasingly important for companies to analyze the personality and behavior of their customers so that they can modify the products according to the market needs and target the customers that will bring the most benefits to them. For instance, it is costly to advertise a new product to everyone, so the company can use the analysis of customers to advertise only to groups that are more likely to make a purchase or accept offers in a market campaign.

In this project, we explore 4 questions to better understand customer personality in the market.
-  Is there a difference in the means of continuous features (age, income...) between the group of customers accepting the discount offer and those not accepting, and between the groups of high and low spending customers?
-  Is there a difference in the means of categorical features (income and spending situation, graduated or not, discount campaign 1-5 accepted or not) between the group of customers accepting the discount offer and those not accepting, and between the groups of higher and lower spending customers?
-  To what extent can we use income and the number of total purchases of a customer to predict the total amount of spending?
-  What is the best fit to predict whether customers accept discount offers in the last campaign?

## Dataset
We used the dataset _marketing_campaign.csv_. It contains 2240 rows and 28 columns. Each row shows the information of one particular customer and the first column represents a unique customer ID. The rest columns contain specific customer features like education, income, the amount spent on several categories of products, and whether they accepted promotions in six campaigns.

## Some Result Graphs
<img width="500" alt="Screenshot 2023-05-30 at 11 25 21" src="https://github.com/MeiyuLiT/Customer-Personality-Analysis/assets/75913591/eb42e71f-d044-442f-a814-76602283cbb2">

<img width="600" alt="Screenshot 2023-05-30 at 11 26 17" src="https://github.com/MeiyuLiT/Customer-Personality-Analysis/assets/75913591/5589f3b5-eae2-40e2-ac27-2d6918862054">

<img width="600" alt="Screenshot 2023-05-30 at 11 26 52" src="https://github.com/MeiyuLiT/Customer-Personality-Analysis/assets/75913591/e787b817-531c-4602-a777-980ac9d1550a">

<img width="600" alt="Screenshot 2023-05-30 at 11 27 13" src="https://github.com/MeiyuLiT/Customer-Personality-Analysis/assets/75913591/36e27fa9-2f47-4b2f-9e38-fe3bffe23665">

<img width="600" alt="Screenshot 2023-05-30 at 11 27 33" src="https://github.com/MeiyuLiT/Customer-Personality-Analysis/assets/75913591/0f45e43c-de22-4324-bcf5-7aaf952c8e09">


## Code
The code is divided into 5 parts: data preprocessing, exploratory analysis, statistical inference, prediction, and classification. 
- **Data Preprocessing**: Considering the low percent of missing values (1%) and outliers (0.01%), we decide to delete them. 
- **Exploratory Analysis**: We plot **bar plots** to see the distribution of categorical variable, **correlation heat map** to see the relationship between continuous features. In addition we perform dimension reduction on selected columns of the raw data before doing our analysis. We choose to apply **PCA** with Kaiser Criterion, and the resulting Scree plot indicates that the first nine principal components play a major role, which explains 69.36% of total variances.
- **Statistical Inference**: The powerful tool _tableone_ gives a convenient way to conduct hypothesis test on both categorical and continuous features. 
  - For continuous variables, we conduct **Two-Sample T-Tests** for the continuous features, because (1) the data has an approximately normal distribution, (2) each feature’s ratio of the variance between each group is less than 1, and (3) customers are independent of each other.
  - For categorical variables, we mostly used **chi-square test** when comparing higher spending and lower spending groups. If the group for some features (eg whether accepting discount campaign) is smaller than 40, we used **Fisher's Exact Test**. 
- **Prediction**: According to the correlation heatmap from Exploratory Analysis and hypothesis testing results from the Statistical Inference Section, we select a set of features that could serve as potential predictors of total amount of spending.
  -  We build **simple linear regression models** for each of them and output the following table with each one of the potential predictors with their associated COD (Coefficient of Determinant)values and beta coefficients.
  -  To avoid overfitting, We try **ridge and lasso regularized regression** to see whether there's any performance improvement of our model. For both Ridge and Lasso, we use grid search with cross validation to find the best hyperparameter.
- **Classification**: Based on the analysis in the inference section, there exist strong correlations between customer personality and their behavior of accepting discounts.
  - To avoid overfitting, we apply **Lasso Regression** to **select significant features**. Specifically, we fit a **logistic regression model** with L1 penalty to find a sparse solution of coefficients while making classification. 
  - To improve the classification performance, we try two more kinds of models that are robust to the imbalance problem, **Random Forest** and **Multi-Layer Perceptron**.
