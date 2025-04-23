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
    <li>

  `rating`: rating given for recipe</li>
    <li>
    `review`: review given for recipe</li>
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

<div style="overflow-x:auto; max-width:800px; font-size:12px;">

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>name</th>
      <th>id</th>
      <th>minutes</th>
      <th>contributor_id</th>
      <th>submitted</th>
      <th>tags</th>
      <th>n_steps</th>
      <th>steps</th>
      <th>description</th>
      <th>ingredients</th>
      <th>n_ingredients</th>
      <th>user_id</th>
      <th>recipe_id</th>
      <th>date</th>
      <th>rating</th>
      <th>review</th>
      <th>avg_rating</th>
      <th>calories</th>
      <th>total_fat</th>
      <th>sugar</th>
      <th>sodium</th>
      <th>protein</th>
      <th>saturated_fat</th>
      <th>carbohydrates</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1 brownies in the world    best ever</td>
      <td>333281</td>
      <td>40</td>
      <td>985201</td>
      <td>2008-10-27</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']</td>
      <td>10</td>
      <td>['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']</td>
      <td>these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!</td>
      <td>['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']</td>
      <td>9</td>
      <td>386585.0</td>
      <td>333281.0</td>
      <td>2008-11-19</td>
      <td>4.0</td>
      <td>These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.</td>
      <td>4.0</td>
      <td>138.4</td>
      <td>10.0</td>
      <td>50.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>19.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <td>1 in canada chocolate chip cookies</td>
      <td>453467</td>
      <td>45</td>
      <td>1848091</td>
      <td>2011-04-11</td>
      <td>['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']</td>
      <td>12</td>
      <td>['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft &amp; chewy in the center', 'serve hot and enjoy !']</td>
      <td>this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.</td>
      <td>['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']</td>
      <td>11</td>
      <td>424680.0</td>
      <td>453467.0</td>
      <td>2012-01-26</td>
      <td>5.0</td>
      <td>Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, &amp; I made the whole batch &amp; used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe!</td>
      <td>5.0</td>
      <td>595.1</td>
      <td>46.0</td>
      <td>211.0</td>
      <td>22.0</td>
      <td>13.0</td>
      <td>51.0</td>
      <td>26.0</td>
    </tr>
    <tr>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']</td>
      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>
      <td>['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']</td>
      <td>9</td>
      <td>29782.0</td>
      <td>306168.0</td>
      <td>2008-12-31</td>
      <td>5.0</td>
      <td>This was one of the best broccoli casseroles that I have ever made.  I made my own chicken soup for this recipe. I was a bit worried about the tsp of soy sauce but it gave the casserole the best flavor. YUM!  \nThe photos you took (shapeweaver) inspired me to make this recipe and it actually does look just like them when it comes out of the oven.  \nThanks so much for sharing your recipe shapeweaver. It was wonderful!  Going into my family's favorite Zaar cookbook :)</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']</td>
      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>
      <td>['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']</td>
      <td>9</td>
      <td>1196280.0</td>
      <td>306168.0</td>
      <td>2009-04-13</td>
      <td>5.0</td>
      <td>I made this for my son's first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']</td>
      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>
      <td>['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']</td>
      <td>9</td>
      <td>768828.0</td>
      <td>306168.0</td>
      <td>2013-08-02</td>
      <td>5.0</td>
      <td>Loved this.  Be sure to completely thaw the broccoli.  I didn&amp;#039;t and it didn&amp;#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']</td>
      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>
      <td>['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']</td>
      <td>9</td>
      <td>520830.0</td>
      <td>306168.0</td>
      <td>2017-10-17</td>
      <td>5.0</td>
      <td>5 stars from my husband and son, my toughest critics. I used a 10-oz bag of chopped broccoli and a 10-oz bag of flowerettes which gave it more texture. Very good flavor and the smell while cooking was great. The sauce held it together without overwhelming the broccoli.</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>millionaire pound cake</td>
      <td>286009</td>
      <td>120</td>
      <td>461724</td>
      <td>2008-02-12</td>
      <td>['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less']</td>
      <td>7</td>
      <td>['freheat the oven to 300 degrees', 'grease a 10-inch tube pan with butter , dust the bottom and sides with flour , and set aside', 'in a large mixing bowl , cream the butter and sugar with an electric mixer and add the eggs one at a time , beating after each addition', 'alternately add the flour and milk , stirring till the batter is smooth', 'add the two extracts and stir till well blended', 'scrape the batter into the prepared pan and bake till a cake tester or knife blade inserted in the center comes out clean , about 1 1 / 2 hours', 'cool the cake in the pan on a rack for 5 minutes , then turn it out on the rack to cool completely']</td>
      <td>why a millionaire pound cake?  because it's super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.</td>
      <td>['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']</td>
      <td>7</td>
      <td>813055.0</td>
      <td>286009.0</td>
      <td>2008-04-09</td>
      <td>5.0</td>
      <td>don't let the calories and fat grams scare you off. This is a wonderful recipe and is perfect for the summer cook-out topped with fresh berries! It will make you proud. This is meant to be shared!</td>
      <td>5.0</td>
      <td>878.3</td>
      <td>63.0</td>
      <td>326.0</td>
      <td>13.0</td>
      <td>20.0</td>
      <td>123.0</td>
      <td>39.0</td>
    </tr>
    <tr>
      <td>2000 meatloaf</td>
      <td>475785</td>
      <td>90</td>
      <td>2202916</td>
      <td>2012-03-06</td>
      <td>['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']</td>
      <td>17</td>
      <td>['pan fry bacon , and set aside on a paper towel to absorb excess grease', 'mince yellow onion , red bell pepper , and add to your mixing bowl', 'chop garlic and set aside', 'put 1tbsp olive oil into a saut pan , along with chopped garlic , teaspoons white pepper and a pinch of kosher salt', 'bring to a medium heat to sweat your garlic', 'preheat oven to 350f', 'coarsely chop your baby spinach add to your heated pan , stir frequently for approximately 5 min to wilt', 'add your spinach to the mixing bowl', 'chop your now cooled bacon , and add it to the mixing bowl', 'add your meatloaf mix to the bowl , with one egg and mix till thoroughly combined', 'add your goat cheese , one egg , 1 / 8 tsp white pepper and 1 / 8 tsp of kosher salt and mix till thoroughly combined', 'transfer to a 9x5 meatloaf pan , and cook for 60 min or until the internal temperature is at least 160f', 'let stand for 5min', 'melt 1tbsp unsalted butter into a frying pan , and cook up to three eggs at a time', 'crack each egg into a separate dish , in order to prevent egg shells from reaching the pan , then add salt and pepper to taste', 'wait until the egg whites are firm looking , but slightly runny on top before flipping your eggs', 'after flipping , wait 10~20 seconds before removing each egg and placing it over your slices of meatloaf']</td>
      <td>ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.</td>
      <td>['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil']</td>
      <td>13</td>
      <td>2204364.0</td>
      <td>475785.0</td>
      <td>2012-03-07</td>
      <td>5.0</td>
      <td>Delicious!!!!! -- the goat cheese made the difference.  My new favorite meatloaf.</td>
      <td>5.0</td>
      <td>267.0</td>
      <td>30.0</td>
      <td>12.0</td>
      <td>12.0</td>
      <td>29.0</td>
      <td>48.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>2000 meatloaf</td>
      <td>475785</td>
      <td>90</td>
      <td>2202916</td>
      <td>2012-03-06</td>
      <td>['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']</td>
      <td>17</td>
      <td>['pan fry bacon , and set aside on a paper towel to absorb excess grease', 'mince yellow onion , red bell pepper , and add to your mixing bowl', 'chop garlic and set aside', 'put 1tbsp olive oil into a saut pan , along with chopped garlic , teaspoons white pepper and a pinch of kosher salt', 'bring to a medium heat to sweat your garlic', 'preheat oven to 350f', 'coarsely chop your baby spinach add to your heated pan , stir frequently for approximately 5 min to wilt', 'add your spinach to the mixing bowl', 'chop your now cooled bacon , and add it to the mixing bowl', 'add your meatloaf mix to the bowl , with one egg and mix till thoroughly combined', 'add your goat cheese , one egg , 1 / 8 tsp white pepper and 1 / 8 tsp of kosher salt and mix till thoroughly combined', 'transfer to a 9x5 meatloaf pan , and cook for 60 min or until the internal temperature is at least 160f', 'let stand for 5min', 'melt 1tbsp unsalted butter into a frying pan , and cook up to three eggs at a time', 'crack each egg into a separate dish , in order to prevent egg shells from reaching the pan , then add salt and pepper to taste', 'wait until the egg whites are firm looking , but slightly runny on top before flipping your eggs', 'after flipping , wait 10~20 seconds before removing each egg and placing it over your slices of meatloaf']</td>
      <td>ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.</td>
      <td>['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil']</td>
      <td>13</td>
      <td>2216720.0</td>
      <td>475785.0</td>
      <td>2012-03-21</td>
      <td>5.0</td>
      <td>What a fabulous recipe. I have a lot of friends who either love to cook, are cookbook authors, are on TV with a cooking show, or who have been featured on cooking shows, so I know a thing or two about cooking. I know, for instance that cooking offers up a continual stream of adventures that do not require a passport or long airline layovers. Cooking is creative, expressive and comforting. A form of open eyed meditation lifting one beyond the commonplace. I'm a vegetarian, but I love to visit other recipes for inspiration so that I can use them by adapting the meat ingredients and therefore adopting them into my favorite recipe file.  All thumbs up for this recipe by an obviously gifted, dedicated and creative cook!</td>
      <td>5.0</td>
      <td>267.0</td>
      <td>30.0</td>
      <td>12.0</td>
      <td>12.0</td>
      <td>29.0</td>
      <td>48.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>5 tacos</td>
      <td>500166</td>
      <td>20</td>
      <td>2549237</td>
      <td>2013-05-13</td>
      <td>['weeknight', '30-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'occasion', 'main-dish', 'beef', 'vegetables', 'easy', 'diabetic', 'dinner-party', 'kid-friendly', 'stove-top', 'dietary', 'comfort-food', 'inexpensive', 'ground-beef', 'meat', 'greens', 'lettuces', 'tomatoes', 'taste-mood', 'equipment', '3-steps-or-less']</td>
      <td>5</td>
      <td>['cook meat', 'add taco seasoning', 'place meat into taco shells / tortillas', 'top with tomatoes , onions , lettuce , salsa and cheese', 'boil corn cobs 5-7 minutes']</td>
      <td>costs about $5.00 to make.</td>
      <td>['ground beef', 'taco seasoning', 'taco shells', 'lettuce', 'tomatoes', 'onion', 'salsa', 'cheddar cheese', 'corn cobs']</td>
      <td>9</td>
      <td>369715.0</td>
      <td>500166.0</td>
      <td>2013-06-13</td>
      <td>4.0</td>
      <td>I doubled the recipe for my family but used two pounds of meat instead of 1.5 pounds. I followed the recipe except we did not use the onions and topped them with sour cream. I also didn&amp;#039;t make the corn. We all enjoyed these.</td>
      <td>4.0</td>
      <td>249.4</td>
      <td>26.0</td>
      <td>4.0</td>
      <td>6.0</td>
      <td>39.0</td>
      <td>39.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>


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

Explanation: From this scatter plot we see how most recipes are around 10,000 calories even as the number of ingrediants increases showcasing how ingrediants aren't may not be majorly relevant to the number of calories in a recip
e. However, we also noticed how in a few cases as ingrediants increase the calorie count reduces which seemed not as intuitive for our team. 

<h3> Interesting Aggregates </h3>

| prep_time_group   |   calories |   total_fat |   sugar |   sodium |   protein |   saturated_fat |   carbohydrates |
|:------------------|-----------:|------------:|--------:|---------:|----------:|----------------:|----------------:|
| 0–15 min          |     301.65 |       23.45 |   66.56 |    27.42 |     16.57 |           27.07 |           10.09 |
| 16–30 min         |     369.7  |       27.96 |   45.72 |    23.77 |     31.31 |           33.47 |           11.42 |
| 31–60 min         |     432.15 |       33.04 |   60.68 |    27.09 |     34.56 |           42.44 |           13.67 |
| 61–120 min        |     564.28 |       43.7  |   95.62 |    32.61 |     40.69 |           56.51 |           18.51 |
| 120+ min          |     547.51 |       39.85 |   68.84 |    47.69 |     57.29 |           48.27 |           15.66 |

Significance: We wanted to build this pivot table in order to do some exploratory data analysis. We wanted to uncover interesting patters or insights in our datasets. From this we could see if calories were impacted by how long something needed to cook. A lot of south asian dishes require extended prep times so we wanted to see if general prep time of many different recipes had any impact on calories. We didn't see any inherent patterns but we saw that sodium content was pretty high. 

<h3> Imputation </h3>

Prior to imputation there were missing values in `name`, `description`,`user_id`, `recipe_id`, `date`, `rating`, `review` and `avg_rating`. This presented as opportunities for our team to impute these values. We decided tat iconstant mputation was only necessary fror `name`, `description`,`user_id`, `recipe_id`, `date`, and `review`. This is mainly because of the nature of the variables as textual (categ)rical variables filling them in with text indicating "No ___ were provided." would not change the data in any fundamental way and for our analysis they weren't very relevant. 

We decided to not impute `rating` and `avg_rating` as these values were integral to our analysis and numerical. If we were to impute these values through mean imputation it would not be an accurate representation of the inputted values by the reviwer. This would likely introduce bias and change overall data analysis in an unpredictable way. 

<h2>Framing a Prediction Problem</h2>

<h3>Prediction Problem</h3>
We are aiming to predict the calorie content of a recipe based on it's nutritional components (example: 
total fat, sugar, carbohydrates, etc.)

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
We built a baseline <strong>linear regression model</strong> to predict the number of calories in recipe based on two nutritional components (carbohydrates, total fat). 

<h3>Features</h3>

<h4>Quantative Features</h4>

`carbohydrates`: Sugar content in Percent Daily Value (PDV%) <br></br>
`total_fat`: Total Fat in Percent Daily Value (PDV%)
<h4>Nominal Features</h4>
None
<h4>Ordinal Features</h4>
None
<h4>Response Varaible</h4>

`calories`: Calorie content, measured as a continous value

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

`sugar_to_protein_ratio`: The ratio captures the ratio between sugar and protein in a recipe. High sugar to protein ratios indicate calorie-dense dessets, while lower ratio's are more protein-rich and possibly more healthier. This ratio might signify more than just taking sugar and protein. 

`total_macro_sum`: This is the sum of six of the nutrional component (total fat, sugar, sodium, protein, statured_fat, carbohydrates). All calories come directly from the nutrional components. This feature acts as a overall proxy for nutrient density. 




<h4>Quantative Features</h4>

`carbohydrates`: Sugar content in Percent Daily Value (PDV%)
`total_fat`: Total Fat in Percent Daily Value (PDV%)
<h4>Engineered Features</h4>

`sugar_to_protein_ration`: The ration of sugar to protein in a recipe
<br></br>

`total_macro_sum`: The sum of six key nutrient components
<h4>Nominal Features</h4>
None
<h4>Ordinal Features</h4>
None
<h4>Response Varaible</h4>

`calories`: Calorie content, measured as a continous value

<h3>Modeling Algorithm</h3>
We used a Random Forest Regressor, choosen for it's ability to be robust to outliers and irrelevant features, and capture non-linear relationships between nutrients and calories. 

<h4>Hyperparameter Tuning</h4>

When tuning our Random Forest Regressor we wanted to choose hyperparameters that are high-impact and worth tunning. We chose these following hyperparamters to tune:
<ul>
    <li>n_estimators - Numbers of trees (more trees means better performance)</li>
    <li>max_depth - Maximum depth of each tree (too depth means overfitting of model and too shallow mean underfitting)</li>
</ul>

<h3>Best Hyperparamters</h3>
<ul>
    <li>n_estimators: 100 </li>
    <li>max_depth: None</li>
</ul>

Our model performs best with 100 grown trees allowing it to capture complex patterns in the data. The no limit on the tree depth, allows for the model to learn complex relationships. 

<h3>Model's Performance and Evaluation</h3>
MSE: 5336.18 <br></br>
MAE: 21.37

MAE dropped by ~62%, and our model on average is only off by about 21 calories. The descrease in the MSE score (~47% lower) also shows that the model is doing better on outliers. The final model captures general patterns.
