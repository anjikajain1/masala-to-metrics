# masala-to-metrics

<h1>Masala to Metrics: Predicting Calories</h1>

Name: Anjika Jain & Riya Bhivare

Email: anjika@umich & rbhiv@umich.edu

Website Link: https://anjikajain1.github.io/masala-to-metrics/

<h2>Introduction</h2>
<h3>Background</h3>

The dataset we chose was Recipes and Ratings. These 2 datasets were scrapped from food.com, a popular online platform for sharing a discovering new recipes. The datasets we worked with were divided in two main components. 

RAW_recipes.csv: Contains all details about recipes, including preparation time, number of steps in recipe, and nutritional information.

RAW_interactions.csv: Includes user reviews and ratings for recipes found in RAW_recipes.csv

Question: What are the different aspects that could impact the calorie content of recipes?

While keeping this question as our focus point we analyzed many properties revolving around calories, such as the distribution of calories in the recipes given and distribution of different nutritional information as well. 

This question was interesting to us, because coming from two south asian households, we have seen that it can be difficult to track calories in some of the recipes that are often meals in our culture. Understanding calorie content can help user cook recipes that meet their dietary goals. It can also help to give food.com's recommendation system to filter by calories considerations. 

<h4> DataSet </h4>

Rows in RAW_recipes: 83,782
Rows in RAW_interactions: 731,927

Columns in RAW_recipes:
<ul>
    <li>rating: rating given for recipe</li>
    <li>review: review given for recipe</li>
</ul>

Columns in RAW_recipes:
<ul>
    <li>name: Recipe name</li>
    <li>minutes: Amount of time to prepare the recipe</li>
    <li>Categories and words assgined to recipes, such as "vegetarian"</li>
    <li> Nutrition: Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”</li>
    <li>n_steps: number of steps in recipe</li>
    <li>description: user description of recipe</li>
</ul>



<h2>Data Cleaning and Exploratory Data Analysis</h2>

<h3>Introduction</h3>



<h3> Data Cleaning </h3>

<h3> Univariate Analysis </h3>
 <iframe
 src="assets/Distribution-of-Calories.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

<iframe
 src="assets/Distribution-of-Total-Fat-Across-All-Recipes.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>
 
<h3> Bivariate Analysis </h3>

 <iframe
 src="assets/Calories-vs-Number-of-Ingredients.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>


 <iframe
 src="assets/Calories-vs-Recipe-Preparation-Time.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

<h3> Interesting Aggregates </h3>
'| prep_time_group | calories | total_fat | sugar | sodium | protein | saturated_fat | carbohydrates |\n| --- | --- | --- | --- | --- | --- | --- | --- |\n| 0–15 min | 301.65 | 23.45 | 66.56 | 27.42 | 16.57 | 27.07 | 10.09 |\n| 16–30 min | 369.7 | 27.96 | 45.72 | 23.77 | 31.31 | 33.47 | 11.42 |\n| 31–60 min | 432.15 | 33.04 | 60.68 | 27.09 | 34.56 | 42.44 | 13.67 |\n| 61–120 min | 564.28 | 43.7 | 95.62 | 32.61 | 40.69 | 56.51 | 18.51 |\n| 120+ min | 547.51 | 39.85 | 68.84 | 47.69 | 57.29 | 48.27 | 15.66 |'

<h3> Imputation </h3>

<h2>Framing a Prediction Problem</h2>


<h2>Baseline Model</h2>


<h2>Final Model</h2>
