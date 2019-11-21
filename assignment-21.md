# Challenge #21 - The Great Codeville Bake-off ([link](https://coding-challenge.lighthouselabs.ca/challenge/21))

The town festival is tomorrow and the organizers have only just realized that they've booked two bakeries to cater desserts, but only have one kitchen available. Instead of just choosing one bakery, let's help them figure out a way to work together.

Both of bakeries have a specialty, so they have each have a stock of specific ingredients.

Lucky for the festival organizers, we've found a recipe book in the town library with TONS of fusion recipes, unfortunately it's 1000 of pages long and we don't have much time. Let's write a function that helps determine which recipes match the ingredients that both bakeries have in stock.

## Instructions

We need to complete a function called chooseRecipe(), which will receive three parameters:

1. An array of ingredients in stock at Bakery A
2. An array of ingredients in stock at Bakery B
3. An array of recipe objects. Each recipe has a name property(string) and an ingredient property(array)

We are limiting our search to two ingredient recipes. We want to find a recipe that utilizes one ingredient from Bakery A and one from Bakery B.

Our `chooseRecipe()` function should return the name of the correct recipe.

Note: In the tests there will always be a single correct answer, and you will NOT need to consider special cases. For example, you do NOT need to worry about cases where one bakery has BOTH the ingredients for a recipe.

## Examples

Input:

```js
const bakeryA = ["saffron", "eggs", "tomato paste", "coconut", "custard"];
const bakeryB = ["milk", "butter", "cream cheese"];
const recipes = [
  {
    name: "Coconut Sponge Cake",
    ingredients: ["coconut", "cake base"]
  },
  {
    name: "Persian Cheesecake",
    ingredients: ["saffron", "cream cheese"]
  },
  {
    name: "Custard Surprise",
    ingredients: ["custard", "ground beef"]
  }
];
```

Output:

```js
Persian Cheesecake
```

## Resolution:

Based on the requirements, the problems to solve are the following:

- Iterate over the recipes
- Per recipe, check whether bakeryA has the _first_ ingredient and bakeryB has the _second_ ingredient
- Or: check whether bakeryA has the _second_ ingredient and bakeryB has the _first_ ingredient
- If so, then we've found a match and can return the `name` of the recipe.

Basically, these steps are translated directly into code. Another `.reduce` method to iterate over the recipes. The `if` statement looks up the ingredients per recipe for both the `bakeryA` collection as the `bakeryB` collection. There are ways to abstract the function some more, where we could check longer lists of ingredients or more bakeries, but for current purposes, this is fine and, also important, **readable** code.

```js
const chooseRecipe = function(bakeryA = [], bakeryB = [], recipes = []) {
  return recipes.reduce((selected, current) => {
    const ingredients = current.ingredients || [];

    if (
      (bakeryA.includes(ingredients[0]) && bakeryB.includes(ingredients[1])) ||
      (bakeryA.includes(ingredients[1]) && bakeryB.includes(ingredients[0]))
    ) {
      selected = current.name;
    }

    return selected;
  }, "");
};
```
