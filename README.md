# Amazon Rating Sales

## Overview
This project aims to analyze products, ratings, prices in the Amazon Sales Data. The purpose of this project is to get comprehensive analysis of Amazon sales data to uncover trends, patterns, and actionable insights. This analysis explores customer behaviors, rating sales, and key business metrics to drive data-driven decision-making.

## Research Question
1. What is the average of all products by category?
2. What is the relationship between the discounted price and the number of ratings?
3. What are the Top 5 Ranking Products Based on Categories?
4. What are the Lowest 5 Ranking Products Based on Categories?

## Tools
Programming Language: Python
Libraries:
  - Pandas: For data manipulation and analysis.
  - Matplotlib/Seaborn: For data visualization.
  - NumPy: For numerical operations.

To view the initial data exploration, click here:
[1_EDA_intro](Python_Data_Project/3_Project/1_EDA_intro.ipynb)

---

# The Analysis
## 1. What is the average of all products by category?
To identify and calculate all rating products by category, i use scatter plot to show how distribution the product based on rating and rating count by category. This visualization can be easily to understand with coloring the plot by category.
### Data Visualization and Results
```python
hue_colors={"Car&Motorbike":"blue", 
            "Computers&Accessories":"green",
            "Electronics":"red",
            "Health&PersonalCare":"cyan",
            "Home&Kitchen":"magenta",
            "HomeImprovement":"yellow",
            "MusicalInstruments":"black",
            "OfficeProducts":"olive",
            "Toys&Games":"grey"}
sns.scatterplot(x="rating", y="rating_count", data=df, hue="product_category", palette=hue_colors)
plt.show()
```
![Visualization of all product based on rating and rating count by categories]([Amazon_Rating_Sales/Image/average of all products.png](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/main/Images/average%20of%20all%20products%20.png))
<br> *Visualization of all product based on rating and rating count by categories*
  
### Insights into Probabilities of Top Skills appearing in Job Posts for Entry Level Data Roles
#### Key Observations:
#### Key Analysis:
### Summary

## 2. What is the relationship between the discounted price and the number of ratings?
To see how far the effect from the relationship is to getting insgiht for better action.
### Data Visualization and Results
```python
hue_colors={"Car&Motorbike":"blue", 
            "Computers&Accessories":"green",
            "Electronics":"red",
            "Health&PersonalCare":"cyan",
            "Home&Kitchen":"magenta",
            "HomeImprovement":"yellow",
            "MusicalInstruments":"black",
            "OfficeProducts":"olive",
            "Toys&Games":"grey"}
sns.scatterplot(x="rating_count", y="discounted_price", data=df, hue="product_category", palette=hue_colors)
plt.show()
```
## 3. What are the Top 5 Ranking Products Based on Categories?
## 4. What are the Lowest 5 Ranking Products Based on Categories?
