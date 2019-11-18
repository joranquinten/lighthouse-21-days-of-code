# Challenge #17 - We're Rooting For You! ([link](https://coding-challenge.lighthouselabs.ca/challenge/17))

At this year's town festival the Codeville Vegetation Association will be handing out several awards for the best vegetables in a given category. We'll be testing out a new judging system on the best tomatoes to start, which can be judged based on their redness OR their plumpness.

## Instructions

For this challenge, we'll need to implement a function called `judgeVegetable()` that will decide which vegetable is best based on a given judging characteristic. Our function will receive two parameters: a list of veggies(as an array of objects), and a characteristic to judge the veggies by (in the case of a tomato, either redness or plumpness).

Our function must return the name of the person who submitted (`vegetables.submitter`) the vegetable with the highest ranking in the provided category.

## Examples

Input:

```js
const vegetables = [
  {
    submitter: "Old Man Franklin",
    redness: 10,
    plumpness: 5
  },
  {
    submitter: "Sally Tomato-Grower",
    redness: 2,
    plumpness: 8
  },
  {
    submitter: "Hamid Hamidson",
    redness: 4,
    plumpness: 3
  }
];

const metric = "redness";
```

Output:

```js
Old Man Franklin
```

## Resolution:

The problems we need to solve are the following:

- Determine a property to compare dynamically
- Iterate over the entries to find the winner

For determining the property, we can note the metric between square brackets (`[]`) to address a dynamic property. Since objects don't really fail gracefully, I've wrapped the function in a `try {} catch() {}` statement. Furthermore, we can use a `.reducer` function (see how versatile that is?) to iterate over the entries and find the winner. We start with no winners (`null`) and automatically assign the first entry as a winner. For every other iteration, we check whether the `metric` on the winner is lower than the current `entry`. If it is, then we have a new runner up and store it in the `winner` variable.

```js
const judgeVegetable = (vegetables = [], metric = "") => {
  try {
    const winner = vegetables.reduce((winner, entry) => {
      if (!winner) {
        winner = entry;
      } else if (winner[metric] < entry[metric]) {
        winner = entry;
      }
      return winner;
    }, null);
    return winner.submitter;
  } catch (e) {
    return null;
  }
};
```
