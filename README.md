![Alt text](readme_images/cover.jpg?raw=true)

# Data-Driven Cocktails

The world of craft cocktails is mysterious. Cocktail books often boast thousands of recipes containing exotic spirits, syrups, and combinations of other ingredients, with little theory to support how these recipes were created or why these recipes work.

This project aims to explore craft cocktails through data science to demystify and make sense of this opaque landscape.

Currently, this project is a work in progress, however, this page will act as an expanding list of key insights based on the analysis conducted to date.

## The Analysis

This analysis aims to answer key questions that will provide insight into craft cocktails and, additionally, create numerous useful tools to facilitate further exploration and experimentation:

-   <b>Research Themes</b> (full question list below): We will first aim to better understand the ingredients used in cocktail recipes. What are they? How often are they used? Then we will explore the recipes themselves. How are ingredients combined to form recipes?
    
-   <b>What Can I Make?</b> This simple tool serves to answer a singular, practical question: given my current bar at home, which recipes can I make?
    
-   <b>Optimization Of A Home Bar</b> (aka. “What should I buy?”) Which combination of ingredients yields the greatest number of complete recipes that can be made? Essentially, if you could only buy X bottles, which would be the most optimal so that you can make the greatest number of craft cocktails?
    
-   <b>Recipe Generator:</b> How can the patterns we learn about existing recipes allow us to create new recipe ideas? Similarly, if I like a certain recipe, which other recipes might I like?

## Scope

While the internet has a massive supply of cocktail recipes, the consistency and quality of these recipes is a concern. To truly understand the nature of great craft cocktails, we will only focus on well-known cocktail books written by some of the world’s best bartenders.

Currently, one book has been implemented - the famous Death & Co. recipe book - however, more books will inevitably be added to get a more representative sample of craft cocktails. For now, Death & Co.’s breadth (500 recipes) and superior quality serves as an excellent starting point.

## Project Files

All Jupyter notebooks to perform this analysis have been included:

- <b>1-get-recipes</b>: Scrape the Death and Co ebook to extract recipes for analysis. Recipe books such as Death and Co.’s include ingredients, but not generalizations of what those specific ingredients are (“Rittenhouse 100 Bottled in Bond” is really a Rye Whiskey). To reach more meaningful and general conclusions in our analysis, we will also need a product hierarchy that can tell us what each ingredient really is at a higher level.
    
- <b>1-get-ingredients</b>: Scrape [thewhiskyexchange.com](https://www.thewhiskyexchange.com/) and extract their comprehensive list of products (well over 10k) and product hierarchy so that we can effectively generalize recipes.
    
- <b>2-prepare-data</b>: Clean each data frame and fuzzy match ingredients found in recipes with ingredients (and their respective hierarchy) that was scraped from the [thewhiskyexchange.com](https://www.thewhiskyexchange.com/)
    
- <b>3-analysis</b>: Notebook that performs the following:
    
	-  Answer research questions via descriptive statistics
    
	- Create a filterable data frame so that users can find out which recipes can be made at home
    
	- perform optimization to determine which combinations of ingredients will allow a user to make the most number of complete recipes
    
	- Predictive model to generate recipes and recommend similar other recipes
  
Data files have currently been excluded for copyright reasons (however, all notebooks are fully executed and rendered in place, allowing a preview of the code and line-by-line analysis).

## Key Insights

For brevity, only select insights will be examined here. To explore all current insights, please refer to the “3-analysis” notebook.

### Research Questions

#### Part I: The Ingredients
These research questions will focus on what are the ingredients? How often are they used? (for full list of questions and insights, see Python notebook)

- For context, this analysis encompasses 466 recipes.
- Across those recipes, there are 2763 ingredients in total (including duplicates), resulting in a typical recipe containing 6 ingredients. This is more than I personally expected.
- 2763 total ingredients translates to 514 unique ingredients, most of which are Spirits/Liqueurs. While Juices, Syrups, Bitters, and other ingredients are fairly versatile, we see that Spirits/Liqueurs are not -- you will need many different types to make all of these recipes!

![Alt text](readme_images/analysis_1.png?raw=true)

- Shown another way, few ingredients are highly versatile and many are used only a handful of times. We’ll examine the distribution of ingredients across different categories in detail, but some of “all-stars” so far are Lemon Juice (134 recipes), Lime Juice (123), Angostura Bitters (90), and Simple Syrup (78).

![Alt text](readme_images/analysis_2.png?raw=true)

- Top 5 ingredients per ingredient category. We’ll take a look at Spirits/Liqueurs below.

| Ingredient category | Ingredient       | # of recipes |
|---------------------|------------------|--------------|
| Bitters             | Angostura        | 88           |
| Bitters             | Orange           | 34           |
| Bitters             | Mole             | 26           |
| Bitters             | Aromatic         | 15           |
| Bitters             | Whiskey          | 12           |
| Common              | Club Soda        | 45           |
| Common              | Sugar            | 21           |
| Common              | Egg              | 19           |
| Common              | Salt             | 14           |
| Common              | Heavy Cream      | 13           |
| Fresh               | Lemon            | 18           |
| Fresh               | Mint             | 13           |
| Fresh               | Cucumber         | 9            |
| Fresh               | Orange           | 9            |
| Fresh               | Strawberry       | 9            |
| Juice               | Lemon Juice      | 134          |
| Juice               | Lime Juice       | 123          |
| Juice               | Grapefruit Juice | 29           |
| Juice               | Pineapple Juice  | 29           |
| Juice               | Orange Juice     | 17           |
| Syrup               | Simple Syrup     | 78           |
| Syrup               | Honey Syrup      | 33           |
| Syrup               | Cinnamon Syrup   | 27           |
| Syrup               | Demerara Syrup   | 27           |
| Syrup               | Ginger Syrup     | 27           |

- For Spirits/Liqueurs, modifier ingredients such as Vermouths and Fruit/Herb Liqueurs remain the most versatile. As the base spirits in cocktail may change, the modifiers stay the same.

![Alt text](readme_images/analysis_3.png?raw=true)

Due to the large variation in ingredient namings for Garnishes (Lemon twist vs lemon wheel vs lemon peel), we can view an imprecise analytical answer to the question of “which garnishes are the most popular through a word cloud visualization.

![Alt text](readme_images/analysis_4.png?raw=true)

#### Part II: Recipes
These questions will focus on: how are ingredients arranged to form recipes? To explore all current insight, please refer to the “3-analysis” notebook.

- Of the 466 recipes, it is most common to see a recipe with 6 ingredients, and 50% of recipes have between 4-7 ingredients. Some complex recipes (like punches) can have up to 12 ingredients, whereas some very strong-flavored and spirit-forward recipes may have as few as 2!

![Alt text](readme_images/analysis_5.png?raw=true)

- Breaking down this distribution by ingredient category, we can see what typical recipes look like. With certain ingredients categories like Spirits, Juices, and Syrups, it is common to see more than 1 or 2 used in a given recipe. With others, it is slightly more binary. Based on a variation of this analysis, we can conclude that the most typical recipe has template has 3 spirits, 1 syrup, and 1 garnish.

![Alt text](readme_images/analysis_6.png?raw=true)

- (WIP) Numerous types of analysis can be done to estimate how the presence of certain ingredient categories impacts the presence of other ingredient categories (correlation, chi2 hypothesis test, association rules). Below I’ve included a few preliminary bivariate graphs that show a few of the more clear relationships.

![Alt text](readme_images/analysis_7.png?raw=true)

![Alt text](readme_images/analysis_8.png?raw=true)

![Alt text](readme_images/analysis_9.png?raw=true)

### What Can I Make?

Unfortunately, not much of this tool can be shown on a static GitHub page like this one. Currently, the data is appropriately formatted in Python and then exported to Google Sheets where a user can easily interact with it to see which recipes they can actually make at home!

### Optimize A Home Bar

Given a budget of X Spirits or Liqueurs that one could buy, which combination would permit the most number of complete recipes to be made? A non-linear solver was used to calculate the following results:


| If I can only buy X number of Spirits/Liqueurs... | ...I should buy...                                                                                       | ...so that I can make Y number of complete recipes... |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| 1                                                 | London Dry Gin                                                                                           | 14                                                    |
| 2                                                 | White Rum, London Dry Gin                                                                                | 25                                                    |
| 3                                                 | Other Rum, White Rum, London Dry Gin                                                                     | 36                                                    |
| 4                                                 | Gold Rum, Other Rum, White Rum, London Dry Gin                                                           | 50                                                    |
| 5                                                 | Fruit Liqueur, Vermouth, Bourbon Whiskey, Gold Rum, London Dry Gin                                       | 66                                                    |
| 6                                                 | Rye Whiskey, Herb Liqueur, Fruit Liqueur, Vermouth, Gold Rum, London Dry Gin                             | 87                                                    |
| 7                                                 | Bourbon Whiskey, Rye Whiskey, Herb Liqueur, Fruit Liqueur, Vermouth, Gold Rum, London Dry Gin            | 106                                                   |
| 8                                                 | Other Rum, Bourbon Whiskey, Rye Whiskey, Herb Liqueur, Fruit Liqueur, Vermouth, Gold Rum, London Dry Gin | 123                                                   |


### Generate Recipe Ideas

Using a nearest-neighbor-style collaborative filtering recommender system, we can leverage patterns of which ingredients commonly appear together to build new recipe ideas.

Here is an actual example of the model in action:

-   User inputs a starting ingredient: “Blanco Tequila”
-   Model returns a list of commonly associated ingredients:
    
	-   Salt
	-   Lime Juice  
	-   Beer
	-   Agave Syrup
	-   Fresh Cucumber
	-   Mezcal
	-   Celery Bitters
	-   Simple Syrup
	-   Hot Sauce
	-   Fresh Cilantro
  
-   A cocktail “profile” (distribution of ingredient categories) is chosen at random and filled with the ingredients recommended in the previous step.
	-   This section is a WIP.
    
-   Try the new recipe in real life!

We can also leverage a similar approach and instead ask users to specify a recipe that they like. We can then recommend similar recipes based on their composition. Here is an actual example:

-   User inputs recipe: “Corpse Reviver #2”
-   Model returns list of similar recipes:

	-   20Th Century
	-   The Joy Division
	-   Dick Brautigan
	-   Lucien Gaudin
	-   Lucinos Delight
	-   19Th Century
	-   Aviation
	-   Coffey Park Swizzle
	-   Gonzalez

- We can compare the ingredients of the cocktail we inputted to the ones that were returned to assess the quality of the recommendations.
  - <b>Corpse Reviver #2</b>: Beefeater London Dry Gin, Cointreau, Lillet Blanc (similar to Vermouth), Vieux Pontarlier Absinthe, Lemon Juice
  - <b>20th Century</b>: Beefeater London Dry Gin, Marie Brizard White Crème De Cacao (Liqueur), Cocchi Americano (a Vermouth), Lemon Juice
  - <b>The Joy Division</b>: Beefeater London Dry Gin, Dolin Dry Vermouth, Cointreau, Vieux Pontarlier Absinthe, Garnish: 1 Lemon Twist
  - ...















