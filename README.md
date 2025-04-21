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
    <li> `name` : Recipe name</li>
    <li> `minutes` : Amount of time to prepare the recipe</li>
    <li>Categories and words assgined to recipes, such as "vegetarian"</li>
    <li> `Nutrition` : Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”</li>
    <li> `n_steps` : number of steps in recipe</li>
    <li> `description` : user description of recipe</li>
</ul>



<h2>Data Cleaning and Exploratory Data Analysis</h2>
<!-- Describe, in detail, the data cleaning steps you took and how they affected your analyses. The steps should be explained in reference to the data generating process. Show the head of your cleaned DataFrame (see Part 2: Report for instructions). -->
<h3> Data Cleaning </h3>
Our team performed various steps in the data cleaning process to ensure our dataset was ready to be analyzed: 

First, we performed a left merge between Recipes and Interactions on the recipe ID in order to bridge the two datasets. 

Then, we noted that user ratings of 0 existed and so, we replaced them with NaN so the average rating calculations are not skewed and there is not a downward bias. 

Next, our team found the average rating for each recipe as a series and added it as a column in order to gain a better understanding of the overall merged dataset.

Finally, one of the major data cleaning steps we took involved the `nutrition` column. Our team distributed the lists within the rows in order to seperate aspects of `nutrition` such as calories, total_fat, sugar, sodium, protein, saturated_fat and carbohydrates. 

Below we've shown the `head` of the cleaned Dataframe.

<div style="overflow:auto">

| name                                 |     id |   minutes |   contributor_id | submitted           | tags                                                                                                                                                                                                                        |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | description                                                                                                                                                                                                                                                          | ingredients                                                                                                                                                                    |   n_ingredients |   user_id |   recipe_id | date                |   rating | review                                                                                                                                                                                                                                                                                                                                           |   avg_rating |   calories |   total_fat |   sugar |   sodium |   protein |   saturated_fat |   carbohydrates |
|:-------------------------------------|-------:|----------:|-----------------:|:--------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|----------:|------------:|:--------------------|---------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------:|-----------:|------------:|--------:|---------:|----------:|----------------:|----------------:|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] |        10 | ['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']                                                  | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven! | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] |               9 |    386585 |      333281 | 2008-11-19 00:00:00 |        4 | These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.                                                                                   |            4 |      138.4 |          10 |      50 |        3 |         3 |              19 |               6 |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                               |        12 | ['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center', 'serve hot and enjoy !'] | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                               | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                    |              11 |    424680 |      453467 | 2012-01-26 00:00:00 |        5 | Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, & I made the whole batch & used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe! |            5 |      595.1 |          46 |     211 |       22 |        13 |              51 |              26 |

</div>

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



<h3> Interesting Aggregates </h3>

| prep_time_group | calories | total_fat | sugar | sodium | protein | saturated_fat | carbohydrates |
|:----------------|---------:|----------:|------:|-------:|--------:|--------------:|---------------:|
| 0-15 min        |   288.56 |      9.31 | 32.35 | 385.52 |   11.96 |          5.75 |          32.37 |
| 16-30 min       |   275.30 |      8.70 | 24.29 | 436.91 |   10.05 |          6.25 |          41.43 |
| 31-60 min       |   259.60 |      9.27 | 20.67 | 428.46 |   14.35 |          5.37 |          31.28 |
| 61-120 min      |   243.64 |      9.61 | 27.61 | 385.96 |   15.65 |          4.65 |          29.28 |
| 120+ min        |   245.00 |     10.63 | 21.81 | 382.38 |   15.67 |          4.88 |          29.80 |


<h3> Imputation </h3>

<h2>Framing a Prediction Problem</h2>

<h3>Prediction Problem</h3>
We are aiming to predict the calorie content of a recipe based on it's nutritional components (example: total fat, sugar, carbohydrates, etc.)

<h3>Problem Type</h3>
This is a regression problem because the target, calories, is a continuous numeric value.

<h3>Response Variable</h3>
The response variable we chose is calories. We chose calories because it is an important indicator for indivudals who are tracking their diets for health, fitness, or medical reasons. Understanding how different nutritional components impact calories can give a more hollistic view to eating healthier. 

<h3>Evaluation Metric</h3>
We will be using Mean Absolute Error (MAE), to evaluate our model. It will tell us, on average, how many calories our model's predictions are off by. This is easiter to interpret for any outside users since metrics like RMSE are weighted more towards large errors and R^2 score provides a value which is unitless (not as intuitive). MAE treats all errors equally. 


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

<h2>Final Model</h2>
