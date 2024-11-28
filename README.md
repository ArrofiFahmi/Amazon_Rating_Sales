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

To view the initial data cleaning and manipulation, click here:
[Amazon Sales Data Cleaning and Manipulation](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/b6a965ab5f4b0c407c2baf46aa39b760eac23b45/Amazon%20Data%20Cleaning%20and%20Manipulation.ipynb)

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
#### Key Observations:
  - Rating : The product ratings range from 2.0 to 5.0, with most data points concentrated between 3.5 and 5.0.
  - Rating Count : The number of ratings varies widely, reaching up to 300,000+ for some products.
  - Category Diversity: Different categories, such as Electronics, Home&Kitchen, and Computer & Accesories, dominate the distribution. Each is color-coded for better   distinction.
#### Key Analysis:
  1. Distribution Across Categories:
      - Electronics (red):This category has a strong presence, with some products achieving very high rating counts (above 300,000). These are typically highly rated (4.0–4.5), indicating both popularity and customer satisfaction.
      - Computers&Accessories (green): While not as widespread as Electronics, this category shows consistent ratings between 3.5 and 4.5. Some items have notable review counts (100,000+).
      - Home&Kitchen (pink): Products in this category are clustered between ratings of 3.5 and 4.5, with review counts mostly under 100,000.
  2. High Rating Count Products:
     - A few products, particularly in Electronics and Home & Kitchen, stand out with exceptionally high rating counts, suggesting strong market engagement.
  3. General Trends:
     - A significant proportion of products, across most categories, have ratings clustered around 4.0 to 4.5, which is typical for popular and well-regarded items.
     - Products rated below 3.0 are sparse, indicating that poorly rated products may not gain substantial customer attention.
### Summary
The scatter plot highlights how Amazon product ratings and review counts are distributed across various categories. Electronics and Health&PersonalCare stand out for their popularity, with some products attracting massive customer engagement. Categories like Home&Kitchen show a broad yet moderate performance. This data can be used to identify high-performing categories and pinpoint areas for further improvement or market focus.

## 2. What is the relationship between the discounted percentage and the ratings?
To see how far the effect from the relationship is to getting insgiht for better action.
### Data Visualization and Results
```python
sns.set_theme(style="whitegrid")
plt.figure(figsize=(12, 8))  # Adjust the figure size for better visibility
scatter_plot = sns.scatterplot(x="rating", y="discount_percentage", data=df,
hue="product_category", palette=hue_colors)
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0.)
plt.title("Rating vs Discount Percentage by Product Category", fontsize=16, fontweight='bold')
plt.xlabel("Rating", fontsize=14)
plt.ylabel("Discount Percentage", fontsize=14)
plt.show()
```
![image alt](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/main/Images/Rating%20vs%20Discount%20Percentage%20by%20Product%20Category.png?raw=true)
#### Key Observations:
  - Rating : Product ratings range from 2.0 to 5.0, with the majority concentrated between 3.5 and 4.5.
  - Discounted Percentage : Discount percentages range from 0% to 80%, with many data points around 40% to 60%
  - Category Diversity: Categories such as Electronics, Home & Kitchen, and Computer & Accessories are well-represented, with some variation in their distribution across the discount and rating spectrum.
#### Key Analysis:
  1. Rating Trends Across Discounts:
     - Products with higher ratings (above 4.0) tend to be offered across a wide range of discount percentages, particularly between 20% and 80%.
     - Lower-rated products (below 3.5) are relatively sparse and less likely to have high discount percentages, suggesting limited promotion or demand.
  2. Category Patterns:
     - Electronic: This category dominates across all rating levels but is especially prominent at high ratings (above 4.0) with varied discount percentages, indicating strong performance even with modest discounts.
     - Home & Kitchen: Concentrated in the mid-range ratings (3.5–4.0), with a tendency toward higher discounts (above 40%), suggesting promotions to improve engagement in this category.
  3. Overall Trends:
     - High-discount products (above 60%) are more likely to be associated with high ratings (4.0+), suggesting effective promotional campaigns or that discounts attract higher customer satisfaction.
     - Products with low discounts (below 20%) are present across all ratings but are less common, suggesting discounts play a significant role in boosting product appeal.
### Summary
The scatter plot reveals a positive relationship between higher discounts (40%–80%) and products with higher ratings (4.0+), especially in categories like Electronics and Computer & Accesories. This indicates that effective discounting strategies can enhance product ratings or vice versa. Categories like Home&Kitchen may rely on discounts to drive engagement for mid-rated products, while high-performing products maintain popularity across diverse discount levels.
## 3. What are the Top 5 Ranking Products Based on Categories?
To identify what the product having good rating are and how we can response it. 
### Data Visualization and Results
```python
def plot_top5_product_types(df, category_col, product_col, rating_col, rating_count_col):
    unique_categories = df[category_col].unique()
    other_data = []
    for category in unique_categories:
        df_filtered = df[df[category_col] == category]
        if len(df_filtered) < 3:
            other_data.append(df_filtered)
        else:
            office_cat_grouped = df_filtered.groupby(product_col).agg(
                mean_rating=(rating_col, "mean"),
                total_rating=(rating_count_col, "sum")
            ).sort_values(by="mean_rating",   
            ascending=False).head(5).reset_index()
            sns.set_theme(style="whitegrid")
            plt.figure(figsize=(10, 6))
            bar_plot = sns.barplot(
                data=office_cat_grouped, 
                x="mean_rating", 
                y=product_col, 
                palette="BrBG", 
                edgecolor="darkgrey")
            plt.title(f"Top 5 Product Types by Mean Rating in {category} Category", fontsize=16, fontweight='bold')
            plt.ylabel('Product Type', fontsize=14)
            plt.xlabel('Mean Rating', fontsize=14)
            
            for index, value in enumerate(office_cat_grouped["mean_rating"]):
                bar_plot.text(value, index, round(value, 2), color='black', ha="left", va="center", fontsize=12)
            plt.legend().set_visible(False)
            plt.show()
  if other_data:
          df_other = pd.concat(other_data)
          office_cat_grouped = df_other.groupby(product_col).agg(
           mean_rating=(rating_col, "mean"),
           total_rating=(rating_count_col, "sum")
          ).sort_values(by="mean_rating", ascending=False).head(5).reset_index()
          sns.set_theme(style="whitegrid")
          plt.figure(figsize=(10, 6))
          bar_plot = sns.barplot(
            data=office_cat_grouped, 
            x="mean_rating", 
            y=product_col, 
            palette="BrBG", 
            edgecolor="darkgrey" )
        plt.title("Top 5 Product Types by Mean Rating in Other Categories", fontsize=16, fontweight='bold')
        plt.ylabel('Product Type', fontsize=14)
        plt.xlabel('Mean Rating', fontsize=14)
        for index, value in enumerate(office_cat_grouped["mean_rating"]):
            bar_plot.text(value, index, round(value, 2), color='black', ha="left", va="center", fontsize=12)
        plt.legend().set_visible(False)
        plt.show()
plot_top5_product_types(df, "product_category", "product_type", "rating", "rating_count")
```
![image alt](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/main/Images/Top%205%20Product%20Types%20in%20HomeKitchen%20Category.png?raw=true)

![image alt](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/main/Images/Top%205%20Product%20Types%20in%20Electronic%20Category.png?raw=true)

![image alt](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/main/Images/Top%205%20Product%20Types%20in%20Computer&Accesories%20Category.png?raw=true)

![image alt](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/main/Images/Top%205%20Product%20Types%20in%20Office%20Category.png?raw=true)

![image alt](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/main/Images/Top%205%20Product%20Types%20in%20Other%20Category.png?raw=true)

#### Key Observations:
  1. Home & Kitchen:
     -Top products in this category include SmallApplianceParts&Accessories, PaintingMaterials, CoffeePresses, AirFryers, and Paints.
     -All these products have mean ratings around 4.43 to 4.5, indicating high customer satisfaction.
  2. Electronic:
     -Leading product types are StreamingClients, Film, SurgeProtectors, ScreenProtectors, and DisposableBatteries.
     -Ratings are slightly varied, with StreamingClients at 4.5 and DisposableBatteries at 4.41.
  3. Computer & Accesories:
     -The highest-rated products include Tablets, PowerLANAdapters, Memory, DVICables, and EthernetCables.
     -Tablets are the standout product type with a mean rating of 4.6, exceeding the others in this category.
  4. Office Product:
     -This category has 5 top rating product, including Basic, Scientific, Financial & Bussiness, Wirebound Notebooks, Composition Notebooks.
     -Customer in this category feel satisfy about the product, with responding rating between 4.37-4.5
  5. Other:
     -A category that has products less than 3 merges in this category.
     -The highest rating for this category include Cord Management, Colouring Pens & Markers, Adapters & Multi Outlets, Digital Bathroom Scales, Condenser.
     -Ratings is variated, with Cord Management 4.5 and Condenser 3.9.
#### Key Analysis:
  1. High Rating Across Categories:
     - Across all 5 categories, the top products consistently maintain ratings above 4.4, suggesting strong quality and customer satisfaction.
     - Tablets in the Computers & Accessories category stand out as the highest-rated product among all categories analyzed.
  2. Specific Trends by Category:
     -Home & Kitchen: Product types with utility or creative use, like Coffee Presses and Air Fryers, rank highly, indicating strong demand for functional and innovative products in this category.
     -Electronics: Essential tech-related accessories like Streaming Clients and Surge Protectors dominate, showing consumer reliance on key accessories for electronic setups.
     -Computers & Accessories: Peripheral items like DVI Cables and Ethernet Cables still hold strong ratings, reflecting quality expectations for necessary computing components.
  3. Customer Priorities:
     - Categories with higher technological or practical usage tend to have more tightly clustered high ratings, as seen in Computers & Accessories and Electronics.
     - Aesthetic or creative tools like Painting Materials and Paints in Home & Kitchen maintain high ratings, reflecting niche satisfaction.
     
### Summary
The analysis identifies top-rated product types for Home & Kitchen, Electronics, Office Product, Other, and Computers & Accessories. Products that combine innovation, practicality, or niche creativity tend to achieve the highest customer satisfaction. Among all categories, Tablets in Computers & Accessories achieve the highest mean rating, Basic lead in Office Products, Cord Management lead in Other, while SmallApplianceParts&Accessories lead in Home & Kitchen, and StreamingClients top the list in Electronics. These findings can guide targeted product promotion and development strategies.
## 4. What are the Lowest 5 Ranking Products Based on Categories?
To see what the product are and how we can fix it or giving recommendations
### Data Visualization and Results
```python
def plot_top5_product_types(df, category_col, product_col, rating_col, rating_count_col):
    unique_categories = df[category_col].unique()
    other_data = []
    for category in unique_categories:
        df_filtered = df[df[category_col] == category]
        if len(df_filtered) < 3:
            other_data.append(df_filtered)
        else:
            office_cat_grouped = df_filtered.groupby(product_col).agg(
                mean_rating=(rating_col, "mean"),
                total_rating=(rating_count_col, "sum")
            ).sort_values(by="mean_rating",   
            ascending=True).head(5).reset_index()
            sns.set_theme(style="whitegrid")
            plt.figure(figsize=(10, 6))
            bar_plot = sns.barplot(
                data=office_cat_grouped, 
                x="mean_rating", 
                y=product_col, 
                palette="BrBG", 
                edgecolor="darkgrey")
            plt.title(f"5 Product Types from The Bottom Tier by Mean Rating in {category} Category", fontsize=16, fontweight='bold')
            plt.ylabel('Product Type', fontsize=14)
            plt.xlabel('Mean Rating', fontsize=14)
            
            for index, value in enumerate(office_cat_grouped["mean_rating"]):
                bar_plot.text(value, index, round(value, 2), color='black', ha="left", va="center", fontsize=12)
            plt.legend().set_visible(False)
            plt.show()
  if other_data:
          df_other = pd.concat(other_data)
          office_cat_grouped = df_other.groupby(product_col).agg(
           mean_rating=(rating_col, "mean"),
           total_rating=(rating_count_col, "sum")
          ).sort_values(by="mean_rating", ascending=True).head(5).reset_index()
          sns.set_theme(style="whitegrid")
          plt.figure(figsize=(10, 6))
          bar_plot = sns.barplot(
            data=office_cat_grouped, 
            x="mean_rating", 
            y=product_col, 
            palette="BrBG", 
            edgecolor="darkgrey" )
        plt.title("5 Product Types from The Bottom Tier by Mean Rating in Other Categories", fontsize=16, fontweight='bold')
        plt.ylabel('Product Type', fontsize=14)
        plt.xlabel('Mean Rating', fontsize=14)
        for index, value in enumerate(office_cat_grouped["mean_rating"]):
            bar_plot.text(value, index, round(value, 2), color='black', ha="left", va="center", fontsize=12)
        plt.legend().set_visible(False)
        plt.show()
plot_top5_product_types(df, "product_category", "product_type", "rating", "rating_count")
```
![image alt](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/main/Images/Top%205%20from%20The%20Bottom%20Product%20Types%20by%20Mean%20Rating%20in%20Home&kitchen%20Categories.png?raw=true)
![image alt](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/main/Images/Top%205%20from%20The%20Bottom%20Product%20Types%20by%20Mean%20Rating%20in%20Electronic%20Categories.png?raw=true)
![image alt](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/main/Images/Top%205%20from%20The%20Bottom%20Product%20Types%20by%20Mean%20Rating%20in%20Computer&Accesories%20Categories.png?raw=true)
![image alt](https://github.com/ArrofiFahmi/Amazon_Rating_Sales/blob/main/Images/Top%205%20from%20The%20Bottom%20Product%20Types%20by%20Mean%20Rating%20in%20Offices%20Categories.png?raw=true)

#### Key Observations:
  1. Electronic: Mean ratings range from 3.5 to 3.8. 3D Glasses have the lowest rating (3.5) in this category, while Remote Controls are rated at 3.8.
  2. Home & Kitchen: The bottom five product types by mean rating range from 3.3 to 3.7. With Electric Grinders have the lowest mean rating of 3.3 and Heat Convector products perform slightly better with a mean rating of 3.7.
  3. Computers & Accesories: The bottom five product types have ratings between 3.4 and 3.67. Dust Covers have the lowest rating (3.4), while Printers have the highest (3.67).
  4. Office Products: Mean Ratings for product types has range between 4.1 to 4.25. The lowest rating is Fountain Pens (4.1) and the Notepads & Memobooks are rated at (4.25)
#### Key Analysis:
- Across all categories, specialized or low-use products such as Electric Grinders, 3D Glasses, and Dust Covers tend to have lower ratings. This indicates potential dissatisfaction due to product performance, usability, or perceived value.
- Home & Kitchen shows wider variability, with products like Electric Grinders and Halogen Heaters lagging behind, suggesting potential quality or reliability issues.
- In Electronics, lower ratings in 3D Glasses and Video Cameras might be due to outdated technology or poor user experiences.
- Computers & Accessories products, particularly Dust Covers and PC Headsets, indicate that peripheral or accessory items might not be meeting customer expectations, likely due to issues with durability or fit.
- Office Products category have relatively moderate ratings ranging from 4.1 to 4.25. Despite being at the lower end of the category, the ratings are still above average, indicating overall decent customer satisfaction.
### Summary
Across the three categories, lower ratings are frequently associated with niche, low-demand, or peripheral products. These products may suffer from poor design, quality concerns, or outdated technology. By focusing on improving the quality, usability, and customer experience of products like Electric Grinders, 3D Glasses, and Dust Covers, We can boost customer satisfaction and potentially improve sales performance for underperforming product types. Additionally, customer feedback and market research could be leveraged to address specific product concerns.
