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
- `name` : Recipe name
- `minutes` : Amount of time to prepare the recipe
Categories and words assgined to recipes, such as "vegetarian"
- `Nutrition` : Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”
- `n_steps` : number of steps in recipe
- `description` : user description of recipe




<h2>Data Cleaning and Exploratory Data Analysis</h2>
<!-- Describe, in detail, the data cleaning steps you took and how they affected your analyses. The steps should be explained in reference to the data generating process. Show the head of your cleaned DataFrame (see Part 2: Report for instructions). -->
<h3> Data Cleaning </h3>
Our team performed various steps in the data cleaning process to ensure our dataset was ready to be analyzed: 

First, we performed a left merge between Recipes and Interactions on the recipe ID in order to bridge the two datasets. 

Then, we noted that user `ratings` of 0 existed and so, we replaced them with NaN so the average rating calculations are not skewed and there is not a downward bias. 

Next, our team found the average rating for each recipe as a series and added it as a column in order to gain a better understanding of the overall merged dataset.

Finally, one of the major data cleaning steps we took involved the `nutrition` column. Our team distributed the lists within the rows in order to seperate aspects of `nutrition` such as calories, total_fat, sugar, sodium, protein, saturated_fat and carbohydrates. 

<h3>Below we've shown the `head` of the cleaned Dataframe.</h3>

<div style="overflow-x: auto; max-width: 100%; white-space: nowrap;">| name                                 |     id |   minutes |   contributor_id | submitted           | tags                                                                                                                                                                                                                        |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | description                                                                                                                                                                                                                                                          | ingredients                                                                                                                                                                    |   n_ingredients |   user_id |   recipe_id | date                |   rating | review                                                                                                                                                                                                                                                         |   avg_rating |   calories |   total_fat |   sugar |   sodium |   protein |   saturated_fat |   carbohydrates |
|:-------------------------------------|-------:|----------:|-----------------:|:--------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|----------:|------------:|:--------------------|---------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------:|-----------:|------------:|--------:|---------:|----------:|----------------:|----------------:|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] |        10 | ['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting'] | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven! | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] |               9 |    386585 |      333281 | 2008-11-19 00:00:00 |        4 | These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs. |            4 |      138.4 |          10 |      50 |        3 |         3 |              19 |               6 |</div>

<h3> Univariate Analysis </h3>

 <iframe
 src="assets/Distribution-of-Calories.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>
 
Explanation: From this histogram we see that the majority of recipes have calorie counts under 1000, and it is right skewed. It suggests that most recipes are relatively moderate in calories, and there are less outliers implying that individuals tend to not share recipes higher in calories.

 
<h3> Bivariate Analysis </h3>

 <iframe
 src="assets/Calories-vs-Number-of-Ingredients.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

Explanation: From this scatter plot we see how most recipes are around 10,000 calories even as the number of ingrediants increases showcasing how ingrediants aren't may not be majorly relevant to the number of calories in a recip
e. However, we also noticed how in a few cases as ingrediants increase the calorie count reduces which seemed not as intuitive for our team. 

<h3> Interesting Aggregates </h3>

| prep_time_group | calories | total_fat | sugar | sodium | protein | saturated_fat | carbohydrates |
|:----------------|---------:|----------:|------:|-------:|--------:|--------------:|---------------:|
| 0-15 min        |   288.56 |      9.31 | 32.35 | 385.52 |   11.96 |          5.75 |          32.37 |
| 16-30 min       |   275.30 |      8.70 | 24.29 | 436.91 |   10.05 |          6.25 |          41.43 |
| 31-60 min       |   259.60 |      9.27 | 20.67 | 428.46 |   14.35 |          5.37 |          31.28 |
| 61-120 min      |   243.64 |      9.61 | 27.61 | 385.96 |   15.65 |          4.65 |          29.28 |
| 120+ min        |   245.00 |     10.63 | 21.81 | 382.38 |   15.67 |          4.88 |          29.80 |


<h3> Imputation </h3>

Prior to imputation there were missing values in `name`, `description`,`user_id`, `recipe_id`, `date`, `rating`, `review` and `avg_rating`. This presented as opportunities for our team to impute these values. We decided tat iconstant mputation was only necessary fror `name`, `description`,`user_id`, `recipe_id`, `date`, and `review`. This is mainly because of the nature of the variables as textual (categ)rical variables filling them in with text indicating "No ___ were provided." would not change the data in any fundamental way and for our analysis they weren't very relevant. 

We decided to not impute `rating` and `avg_rating` as these values were integral to our analysis and numerical. If we were to impute these values through mean imputation it would not be an accurate representation of the inputted values by the reviwer. This would likely introduce bias and change overall data analysis in an unpredictable way. 

<h2>Framing a Prediction Problem</h2>

<h3>Prediction Problem</h3>
We are aiming to predict the calorie content of a recipe based on it's nutritional components (example: total fat, sugar, carbohydrates, etc.)

<h3>Problem Type</h3>
This is a regression problem because the target, calories, is a continuous numeric value.

<h3>Response Variable</h3>
The response variable we chose is calories. We chose calories because it is an important indicator for indivudals who are tracking their diets for health, fitness, or medical reasons. Understanding how different nutritional components impact calories can give a more hollistic view to eating healthier. 

<h3>Evaluation Metric</h3>
We will be using Mean Absolute Error (MAE), to evaluate our model. It will tell us, on average, how many calories our model's predictions are off by. MAE treats all errors equally. 

We will also use Root Mean Square Error (RMSE) as it provides an overall sense of prediction error, but will keep in mind that it is weighted more towards large error. 

We will not look at the R^2 score as it isn't intiuative for users, and provides a value which is unitless. 



<h2>Baseline Model</h2>

<h3>Model Description and Features</h3>
<strong>We built a baseline linear regression model</strong> to predict the number of calories in recipe based on two nutritional components (carbohydrates, total fat). 

<h3>Features</h3>

<h4>Quantative Features</h4>
carbohydrates: Sugar content in Percent Daily Value (PDV%)
total_fat: Total Fat in Percent Daily Value (PDV%)
<h4>Nominal Features</h4>
None
<h4>Ordinal Features</h4>
None
<h4>Response Varaible</h4>
calories: Calorie content, measured as a continous value

<h3>Preprocessing Steps</h3>
We defined a sub-pipeline for numerical features, to use SimpleImputer to fill in missing values a replace them with the mean value in each column. 

We evaluated the model on a test set of 20% of the data.

<h3>Model Performance</h3>
MSE Value: 9719.29 (RSME: 98.5)
Interpretation: This measures the average square difference between predicted and actual calorie values. Because the errors are squared it may have penalized larger error more. 

MAE Value: 55.75
This means our baseline model's calorie predictions are off by an average of 55.75 calories.

<h3>Is This a Good Model?</h3>

Based on MAE value of 55.75, if our recipes on average have hundreds of calories being off by 56 could be okay for some users who just want a sort of general understanding of how calorie dense their meals are. However, for users who are looking for accurate predictions an average of 56 calories could be a large issue for them. A MSE value of 9719 is very high, suggesting that the errors that are occuring must be large. Since we use only two features (total_fat + carbohydrates), it is probably not highlighting how all the different nurtrional components (protein, sugar, etc.) impact the calories. This is an okay baseline mode, but not a great model, as we are not super precise. 

<h2>Final Model</h2>

We introduce two engineered features to capture better predictions:

sugar_to_protein_ratio: The ratio captures the ratio between sugar and protein in a recipe. High sugar to protein ratios indicate calorie-dense dessets, while lower ratio's are more protein-rich and possibly more healthier. This ratio might signify more than just taking sugar and protein. 

total_macro_sum: This is the sum of six of the nutrional component (total fat, sugar, sodium, protein, statured_fat, carbohydrates). All calories come directly from the nutrional components. This feature acts as a overall proxy for nutrient density. 




<h4>Quantative Features</h4>
carbohydrates: Sugar content in Percent Daily Value (PDV%)
total_fat: Total Fat in Percent Daily Value (PDV%)
<h4>Engineered Features</h4>
sugar_to_protein_ration: The ration of sugar to protein in a recipe
total_macro_sum: The sum of six key nutrient components
<h4>Nominal Features</h4>
None
<h4>Ordinal Features</h4>
None
<h4>Response Varaible</h4>
calories: Calorie content, measured as a continous value

<h3>Modeling Algorithm</h3>
We used a Random Forest Regressor, choosen for it's ability to be robust to outliers and irrelevant features, and capture non-linear relationships between nutrients and calories. 

<h4>Hyperparameter Tuning</h4>

When tuning a Random Forest Regressor we wanted to choose hyperparameters that are high-impact and worth tunning 

<h3>Model's Performance and Evaluation</h3>
MSE: 5142.83
MAE: 21.36