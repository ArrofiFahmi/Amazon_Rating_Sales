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
![image alt](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/main/Images/average%20all%20of%20product.png?raw=true)
### Insights into Probabilities of Top Skills appearing in Job Posts for Entry Level Data Roles
#### Key Observations:
  - Rating : The product ratings range from 2.0 to 5.0, with most data points concentrated between 3.5 and 5.0.
  - Rating Count : The number of ratings varies widely, reaching up to 400,000+ for some products.
  - Category Diversity: Different categories, such as Electronics, Home&Kitchen, and Health&PersonalCare, dominate the distribution. Each is color-coded for better   distinction.
#### Key Analysis:
  1. Distribution Across Categories:
      - Electronics (red):This category has a strong presence, with some products achieving very high rating counts (above 300,000). These are typically highly rated (4.0–4.5), indicating both popularity and customer satisfaction.
      - Computers&Accessories (green): While not as widespread as Electronics, this category shows consistent ratings between 3.5 and 4.5. Some items have notable review counts (~100,000+).
      - Home&Kitchen (pink): Products in this category are clustered between ratings of 3.5 and 4.5, with review counts mostly under 100,000.
  2. High Rating Count Products:
     - A few products, particularly in Electronics and Health&PersonalCare, stand out with exceptionally high rating counts, suggesting strong market engagement.
  3. General Trends:
     - A significant proportion of products, across most categories, have ratings clustered around 4.0 to 4.5, which is typical for popular and well-regarded items.
     - Products rated below 3.0 are sparse, indicating that poorly rated products may not gain substantial customer attention.
### Summary
The scatter plot highlights how Amazon product ratings and review counts are distributed across various categories. Electronics and Health&PersonalCare stand out for their popularity, with some products attracting massive customer engagement. Categories like Home&Kitchen show a broad yet moderate performance. This data can be used to identify high-performing categories and pinpoint areas for further improvement or market focus.

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
![image alt](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/main/Images/relationship%20between%20the%20discounted%20price%20and%20the%20number%20of%20ratings.png?raw=true)
## 3. What are the Top 5 Ranking Products Based on Categories?
## 4. What are the Lowest 5 Ranking Products Based on Categories?
