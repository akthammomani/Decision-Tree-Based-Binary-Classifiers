# Project: Decision Tree Specialty Coffee

<p align="center">
  <img width="750" height="350" src="https://user-images.githubusercontent.com/67468718/105829430-37fde600-5f79-11eb-8604-257cb2988a07.JPG">
</p>

## 1. Introduction

**RR Diner Coffee** sells two types of thing:
- specialty coffee beans, in bulk (by the kilogram only) 
- coffee equipment and merchandise (grinders, brewing equipment, mugs, books, t-shirts).

RR Diner Coffee has three stores, two in Europe and one in the USA. The flagshap store is in the USA, and everything is quality assessed there, before being shipped out. Customers further away from the USA flagship store have higher shipping charges. 

You've been taken on at RR Diner Coffee because the company are turning towards using data science and machine learning to systematically make decisions about which coffee farmers they should strike deals with. 

RR Diner Coffee typically buys coffee from farmers, processes it on site, brings it back to the USA, roasts it, packages it, markets it, and ships it (only in bulk, and after quality assurance) to customers internationally. These customers all own coffee shops in major cities like New York, Paris, London, Hong Kong, Tokyo, and Berlin. 

Now, RR Diner Coffee has a decision about whether to strike a deal with a legendary coffee farm (known as the **Hidden Farm**) in rural China: there are rumours their coffee tastes of lychee and dark chocolate, while also being as sweet as apple juice. 

It's a risky decision, as the deal will be expensive, and the coffee might not be bought by customers. The stakes are high: times are tough, stocks are low, farmers are reverting to old deals with the larger enterprises and the publicity of selling *Hidden Farm* coffee could save the RR Diner Coffee business. 

So our job here is ***To build a decision tree to predict how many units of the Hidden Farm Chinese coffee will be purchased by RR Diner Coffee's most loyal customers.*** 

To this end, you and your team have conducted a survey of 710 of the most loyal RR Diner Coffee customers, collecting data on the customers':
- age
- gender 
- salary 
- whether they have bought at least one RR Diner Coffee product online
- their distance from the flagship store in the USA (standardized to a number between 0 and 11) 
- how much they spent on RR Diner Coffee products on the week of the survey 
- how much they spent on RR Diner Coffee products in the month preeding the survey
- the number of RR Diner coffee bean shipments each customer has ordered over the preceding year. 

You also asked each customer participating in the survey whether they would buy the Hidden Farm coffee, and some (but not all) of the customers gave responses to that question. 

You sit back and think: if more than 70% of the interviewed customers are likely to buy the Hidden Farm coffee, you will strike the deal with the local Hidden Farm farmers and sell the coffee. Otherwise, you won't strike the deal and the Hidden Farm coffee will remain in legends only. There's some doubt in your mind about whether 70% is a reasonable threshold, but it'll do for the moment. 

To solve the problem, then, you will build a decision tree to implement **a classification solution.**


## 2. Objective

This notebook uses decision trees to determine whether the factors of salary, gender, age, how much money the customer spent last week and during the preceding month on RR Diner Coffee products, how many kilogram coffee bags the customer bought over the last year, whether they have bought at least one RR Diner Coffee product online, and their distance from the flagship store in the USA, could predict whether customers would purchase the Hidden Farm coffee if a deal with its farmers were struck. 

## 3. Sourcing and loading
- Import packages
- Load data
- Explore the data
 
## 4. Cleaning, transforming and visualizing
- Imbalanced Dataset:
  - RR Coffee's Customers who said "Yes", The closer they're from RR Coffeee store the more they spent last month.
  - RR Coffee's Customers who said "No", The closer they're from RR Coffeee store the less they spent last month.
  - The Dataset is imbalanced (303 said 'YES' & 171 said 'NO') and this will affect negatively the Models score accuracy

![Decision](https://user-images.githubusercontent.com/67468718/106380149-33647380-6365-11eb-911c-48f8b8a6e01c.JPG)

- Train/test split  
  
## 5. Modelling 
- **Model 1: Entropy model - no max_depth** 

  - As shown below, we have 9 leaves with purity at 0 (This is the ideal scenario), however 4 of them are having a very low number of samples so we cannot be very confident for their predictions (clear sign of over-fitting).
  - Features used in the splits: spend_last_month, Distance and Age.
  - As shown below, we have a fully grown Decision Tree (none of the parameters were set e.g., max_depth) as a result the tree grows to a fully to a depth of 5. There are 8 nodes and 9 leaves: Not limiting the growth of a Decision Tree will delay reaching the split choices that will get us to the pure nodes (leaves=predictions) causing over-fitting.

![DT_entropy](https://user-images.githubusercontent.com/67468718/106380151-33fd0a00-6365-11eb-8069-18886dc9198b.png)

- **Model 2: Gini impurity model - no max_depth** 

  - As shown below, we have 11 leaves with purity at 0 (This is the ideal scenario), however 6 of them are having a very low number of samples so we cannot be very confident for their predictions (clear sign of over-fitting).
  - Features used in the splits: spend_last_month, Distance, Age and num_coffeeBags_per_year.
  - As shown below, we have a fully grown Decision Tree (none of the parameters were set e.g., max_depth) as a result the tree grows to a fully to a depth of 6. There are 10 nodes and 11 leaves: Not limiting the growth of a Decision Tree will delay reaching the split choices that will get us to the pure nodes (leaves=predictions) causing over-fitting.
  
![DT_gini](https://user-images.githubusercontent.com/67468718/106380152-3495a080-6365-11eb-83d3-a7a323756049.png)

- **Model 3: Entropy model - max depth 3**

  - As shown below, we have 5 leaves with purity at 0 (One Class) with only one leave having a very low number of samples (This is the ideal scenario): The more leaves with purity=0 and high samples the more information gain (more predicition power).
  - Features used in the splits: spend_last_month, Distance, Age and num_coffeeBags_per_year.
  - As shown below, we have a Decision Tree (max_depth=3) as a result the tree grows to a depth of 3. There are 4 nodes and 5 leaves: When limiting the growth of the Decision Tree we find the split choices that will get us to the pure nodes much faster resulting in more information gain (more predicition power).

![entropy_d_3](https://user-images.githubusercontent.com/67468718/106380154-352e3700-6365-11eb-9b0b-677b3b21baed.png)

- **Model 4: Gini impurity model - max depth 3**

  - As shown below, we have 7 leaves with purity at 0 (One Class) with only one leave having a very low number of samples (This is the ideal scenario): The more leaves with purity=0 and high samples the more information gain (more predicition power).
  - Features used in the splits: spend_last_month and Distance (features importance illustrated below).
  - As shown below, we have a Decision Tree (max_depth=3) as a result the tree grows to a depth of 3. There are 6 nodes and 7 leaves: When limiting the growth of the Decision Tree we find the split choices that will get us to the pure nodes much faster resulting in more information gain (more predicition power).

![DT_gini_d_3](https://user-images.githubusercontent.com/67468718/106380153-3495a080-6365-11eb-8097-572b6d44b2e9.png)

- **Why Model 4: Gini impurity model - max depth 3 is the best so far?**

  - Calculation of Entropy & Gini methods behaves in the same way but entropy involves a log computation and Gini impurity involved a square computation. Since computing square is cheaper than logarithmic function we prefer Gini impurity over entropy.
  - We have 7 leaves with purity at 0 (One Class) in Gini compared to only 5 leaves with purity at 0in Entropy: The more leaves with purity=0 and high samples the more information gain (more predicition power).


## 6. Model 5: Random Forest vs Model 4: Gini Impurity 
- Gini impurity  model - max depth 3:
  - Actual Data is distributed as "NO"=41 and "YES"=78
  - TP (True Positives): Model predicted "NO" and it was actually "NO" = 39
  - TN (True Negatives): Model predicted "YES" and it was actually "YES" = 77
  - FN (False Negatives): Model predicted "YES" and it was actually "No" = 2
  - Total "Yes" was 80
  
**<ins>Gini impurity  model - max depth 3:<ins>** **Confusion Matrix Breakdown**

| Metrics | value  |Metrics   | value  | Total  | value  |
|:---:|:---:|:---:|:---:|:---:|:---:|
| TP |  39 | FN  | 2  |Total   | 41  |
| FP |   1|  TN | 77  |Total   | 78  |  

- Random Forest model 5 - max depth 3:
  - Actual Data is distributed as "NO"=41 and "YES"=78
  - TP (True Positives): Model predicted "NO" and it was actually "NO" = 35 (Less than Gini Model)
  - TN (True Negatives): Model predicted "YES" and it was actually "YES" = 77 (Similar to Gini)
  - FN (False Negatives): Model predicted "YES" and it was actually "No" = 6 (Increased by 4 compared to Gini)
  - Total "Yes" was 84
  
**<ins>Random Forest model 5 - max depth 3:<ins>** **Confusion Matrix Breakdown:**

| Metrics | value  |Metrics   | value  | Total  | value  |
|:---:|:---:|:---:|:---:|:---:|:---:|
| TP |  35 | FN  | 6  |Total   | 41  |
| FP |   1|  TN | 77  |Total   | 78  | 

## 7. Final Conclusion
- How many customers will buy Hidden Farm coffee?

  - **Model 5: Random Forests** has shown an increase of the potetial buyers by 3.2% from 183 to 189 potetial buyers and that put us exactly at 70.1 % which is more than indicated 70% of the interviewed customers who are likely to buy the Hidden Farm coffee.
  - According to the above we can encourage ***RR Diner Coffee*** to strike the deal with the local Hidden Farm farmers.


## 8. Why Random Forests outerperform Gini Model2, even with much lower Accuracy?

- Because our Dataset is imbalanced; accuracy should not be used to measure our Models Performance.
- Instead of Accuracy, we need to focus in Confusion Matrix that shows the correct predictions and types of incorrect predictions, as shown below the prediction power of "Yes" has increased in Random Forest compared to Gini Model.
- In addition to confusion matrix we can use ROC AUC from sklearn.metrics to evaluate metrics for calculating the performance of any classification model's performance, as shown below AUC score is signficantly higher in Random Forest compared to Gini Model

|Model|AUC|
|:---:|:-:|
|Random Forest Model|99.4997|
|Gini Model2|98.7023|
|Entropy Model2|97.6548|
|Gini Model|98.1395|
|Entropy Model|98.7805|
