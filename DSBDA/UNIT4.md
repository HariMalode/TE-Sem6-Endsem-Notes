# Unit 4: Predictive big data analytics with Python

### Q1. What is data preprocessing? Explain various data preprocessing steps. Discuss essential python libraries for preprocessing

- Data preprocessing is a crucial step in data science and big data analytics where raw data is transformed into a clean, organized, and structured format suitable for analysis.
- It involves various operations to clean, transform, and prepare the data for analysis, ensuring that the data is of high quality and can be effectively used by machine learning models or other analytical techniques.
- Data preprocessing is essential because real-world datasets are often messy and incomplete.
    Ex, Salary="-3000"(Noisy data), Age="18yrs" with DOB:"11/2/2023"(Inconsistent data),Occupation=""(Incomplete data).

Here are some common data preprocessing steps:

1. **Data Cleaning**:
   - Handling missing values: This involves strategies like imputation (replacing missing values with a calculated value such as mean median mode) or deletion (removing rows or columns with missing values).

2. **Data Transformation**:
   - Converting categorical variables into a numerical format that machine learning algorithms can work with.
   - Data standardization is the process of transforming data such that its mean is 0 and standard deviation is 1.
   - Data normalization, on the other hand, scales the data to a range between 0 and 1. Data normalized by dividing each value by the maximum value in its respective dataset.

3. **Data Reduction**:
   - Dimensionality reduction: Data Reduction used to reduce the number of features while retaining most of the information.

4. **Data Integration**:
   - Combining data from multiple sources into a single dataset, ensuring consistency and compatibility between them.

5. **Data Discretization**:
   - Discretization  used to reduce the number of continuous values in a dataset by dividing them into intervals or categories.

Python offers several libraries for data preprocessing, some of which are widely used in the data science community:

1. **Pandas**: Pandas is a powerful library for data manipulation and analysis. It provides data structures like DataFrames, which are ideal for handling tabular data, and a wide range of functions for data preprocessing tasks such as handling missing values, data transformation, and data cleaning.

2. **NumPy**: NumPy is a fundamental package for scientific computing in Python. It provides support for large, multi-dimensional arrays and matrices, along with a collection of mathematical functions to operate on these arrays efficiently. NumPy is often used in conjunction with Pandas for numerical computations and data manipulation tasks.

3. **Scikit-learn**: Scikit-learn is a machine learning library in Python that provides simple and efficient tools for data mining and data analysis. 

4. **Matplotlib**: These libraries are commonly used for data visualization in Python. Visualizing data is an essential part of the data preprocessing pipeline as it helps in understanding the distribution of data, identifying outliers, and detecting patterns.

By leveraging these libraries effectively, data scientists can preprocess raw data efficiently and prepare it for further analysis or modeling.

---

### Q2. What are association rules ? Explain Apriori algorithm in brief.

Association rules are a type of rule-based technique used in data mining and machine learning to discover interesting relationships or patterns within large datasets. These rules describe the probabilistic relationships between items in a dataset and are often used in market basket analysis, where the goal is to find associations between products that are frequently purchased together.

An association rule typically has two parts:

1. **Antecedent (LHS)**: This is the set of items or itemsets that are present in the rule's condition. It represents the items that act as the premise for the association.

2. **Consequent (RHS)**: This is the item or itemset that is predicted or implied by the antecedent. It represents the item(s) that are likely to be purchased together with the items in the antecedent.

The strength of an association rule is usually measured using metrics like support, confidence, and lift:

- **Support**: This indicates the frequency with which a rule occurs in the dataset. It measures the proportion of transactions in the dataset that contain both the antecedent and consequent. Support is calculated as the ratio of the number of transactions containing both the antecedent and consequent to the total number of transactions in the dataset.(Support =A+B/Total)

- **Confidence**: This measures the reliability or certainty of the rule. It is the ratio of the support of both the antecedent and consequent to the support of the antecedent. (Confidence =A+B/A)

- **Lift**: Lift measures how much more likely the consequent is given the antecedent, compared to its likelihood without the antecedent. It is calculated as the ratio of the confidence of the rule to the support of the consequent. (Lift = Confidence/Support)

Now, let's discuss the Apriori algorithm:

The Apriori algorithm is one of the most popular algorithms for mining association rules. It works by iteratively generating candidate itemsets and pruning those that do not meet the minimum support threshold. The algorithm follows these steps:

1. **Initialization**: The algorithm starts by scanning the dataset to determine the support of each individual item. Items that do not meet the minimum support threshold are discarded.

2. **Generation of Candidate Itemsets**: Based on the frequent itemsets discovered in the previous iteration, the algorithm generates candidate itemsets of larger sizes by joining pairs of frequent itemsets.

3. **Pruning**: Candidate itemsets that do not meet the minimum support threshold are pruned from further consideration.

4. **Repeat**: Steps 2 and 3 are repeated until no new frequent itemsets can be generated.

5. **Rule Generation**: Once all frequent itemsets are discovered, association rules are generated from them by applying a confidence threshold. Only rules with confidence above the threshold are retained.

The Apriori algorithm is efficient for discovering frequent itemsets and association rules in large datasets because of its pruning strategy, which reduces the search space. However, it can still be computationally expensive for very large datasets or datasets with a large number of unique items.

---

### Q3. How Apriori algorithm works, Explain with suitable example

Let's illustrate how the Apriori algorithm works with a simple example of market basket analysis. Imagine you have a dataset containing transactions from a grocery store, where each transaction consists of a set of items purchased by a customer.

Here's a sample dataset:

```
Transaction 1: Bread, Milk
Transaction 2: Bread, Diapers, Beer, Eggs
Transaction 3: Milk, Diapers, Beer, Coke
Transaction 4: Bread, Milk, Diapers, Beer
Transaction 5: Bread, Milk, Diapers, Coke
```

We'll apply the Apriori algorithm to find association rules in this dataset.

**Step 1: Initialization**

In the first step, we determine the support of each individual item. Let's assume our minimum support threshold is 2 (i.e., an item must appear in at least 2 transactions to be considered frequent).

```
Item:        Support:
Bread        4
Milk         4
Diapers      4
Beer         3
Eggs         1
Coke         2
```

We discard Eggs because it doesn't meet the minimum support threshold.

**Step 2: Generation of Candidate Itemsets**

Next, we generate candidate itemsets of size 2 by joining pairs of frequent itemsets. We only consider pairs of items that were frequent in the previous step.

```
Frequent Itemsets of Size 2:
{Bread, Milk}
{Bread, Diapers}
{Bread, Beer}
{Milk, Diapers}
{Milk, Beer}
{Diapers, Beer}
{Diapers, Coke}
```

**Step 3: Pruning**

We prune candidate itemsets that do not meet the minimum support threshold. 

```
Pruned Frequent Itemsets of Size 2:
{Bread, Milk}
{Bread, Diapers}
{Milk, Diapers}
{Diapers, Beer}
{Diapers, Coke}
```

**Step 4: Repeat**

We repeat steps 2 and 3 to generate frequent itemsets of size 3 and beyond. For simplicity, let's consider only frequent itemsets of size 3.

```
Frequent Itemsets of Size 3:
{Bread, Milk, Diapers}
{Milk, Diapers, Beer}
{Diapers, Beer, Coke}
```

**Step 5: Rule Generation**

Finally, we generate association rules from the frequent itemsets by applying a confidence threshold. Let's assume our confidence threshold is 0.5.

```
Association Rules:
{Bread, Milk} -> {Diapers} (Confidence = 3/4 = 0.75)
{Milk, Diapers} -> {Beer} (Confidence = 2/4 = 0.5)
{Diapers} -> {Beer, Coke} (Confidence = 2/4 = 0.5)
```

These are the association rules discovered by the Apriori algorithm in our example dataset. They indicate the likelihood of one itemset leading to the purchase of another itemset. For example, the rule {Bread, Milk} -> {Diapers} suggests that customers who buy Bread and Milk are likely to also buy Diapers, with a confidence of 75%.

---

### Q4. What are the types of analytics in big data? Explain in brief

In big data analytics, there are primarily three types of analytics: descriptive analytics, predictive analytics, and prescriptive analytics. Each type serves a distinct purpose and provides valuable insights to organizations:

1. **Descriptive Analytics**:
   - Descriptive analytics focuses on summarizing historical data to understand what has happened in the past. It involves analyzing data to uncover patterns, trends, and insights that can help in understanding past performance and making data-driven decisions.
   - The descriptive model shows relationships between the customer and product/service
   - Examples of descriptive analytics include generating reports, creating dashboards, and visualizing data through charts and graphs.
   - Descriptive statistics are useful to show things like, total stock in inventory, average dollars spent per customer and Year over year change in sales.
   - What has happened?

2. **Predictive Analytics**:
   - Predictive analytics involves analyzing historical data to make predictions about future events or outcomes. It uses statistical techniques, machine learning algorithms, and data mining to identify patterns and relationships in data that can be used to forecast future trends.
   - Predictive analytics helps your organization predict with confidence what will happen next so that you can make smarter decisions and improve business outcomes
   - Examples of predictive analytics include sales forecasting, demand forecasting, customer churn prediction, and risk assessment.
   - Predictive analytics helps organizations anticipate future events and make informed decisions based on likely outcomes, allowing them to proactively plan and allocate resources.
   - What could happened?

3. **Prescriptive Analytics**:
   - Prescriptive analytics goes beyond predicting future outcomes by providing recommendations or prescriptions for actions to achieve desired outcomes. It combines insights from descriptive and predictive analytics with optimization and simulation techniques to recommend the best course of action.
   - An example of this is a traffic application helping you choose the best route home and taking into account the distance of each route, the speed at which one can travel on each road and, crucially, the current traffic constraints.
   - Larger companies are successfully using prescriptive analytics to optimize production; It helps in the supply chain to make sure that are delivering the right products at the right time and optimizing the customer experience
   - What should we do?

In summary, descriptive analytics helps in understanding what happened, predictive analytics helps in predicting what will happen, and prescriptive analytics helps in determining what actions to take to achieve desired outcomes. By leveraging all three types of analytics, organizations can gain deeper insights into their data, drive innovation, and gain a competitive edge in today's data-driven world.