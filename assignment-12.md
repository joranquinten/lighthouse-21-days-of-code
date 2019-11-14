# Challenge #12 - In the Air Tonight ([link](https://coding-challenge.lighthouselabs.ca/challenge/12))

The citizens of Codeville seem pleased with all the upgrades you're making to the local infrastructure. Next on your list to tackle is the air quality. You've decided that you want to install air pollution sensors around the city to monitor air quality and identify problem areas. We need to write the code for the sensors to trigger a special message when the air is too polluted.

## Instructions

For this challenge we will implement a function called `checkAir()`, which will check a collection of air samples. The function will take in two arguments. The first argument is an array of strings, where each string represents a small air sample that is either `clean` or `dirty`. The second argument is a number representing the highest acceptable amount of dirty samples. For example, a `threshold` of 0.4 means that there must be less than 40% of total samples classified as dirty for our air to be considered clean. Our function must return `Polluted` if there are too many dirty air samples, or `Clean` if the proportion of dirty samples is below the threshold.

## Examples

Input:

```js
const samples = [
  "clean",
  "clean",
  "dirty",
  "clean",
  "dirty",
  "clean",
  "clean",
  "dirty",
  "clean",
  "dirty"
];
const threshold = 0.3;
```

Output:

```js
Polluted;
```

## Resolution:

I've added a bit more comments to the code, to better show what's going on inside of the function. There are three problems to solve:

- Count the samples per given category
- Translate the total to a percentage
- Compage the percentage to the threshold to return the correct return value

I use the `.reducer` method to build up the total. You can see how versatile a `.reducer` can be. If you need to transform an array into any other shape, I always reach for this method.

After you've got the total, it's a matter of some math to translate it to a percentage, compare it to the threshold and you're done!

```js
// Samples is either `clean` or `dirty`
// threshold is the percentage of `dirty` samples
const checkAir = function(samples = [""], threshold = 1) {
  // First count the distribution of samples:
  const distribution = samples.reduce(
    (total, current) => {
      if (current === "clean") {
        total.clean = total.clean + 1;
      }
      if (current === "dirty") {
        total.dirty = total.dirty + 1;
      }
      return total;
    },
    { clean: 0, dirty: 0 }
  );

  // Calculate percentage pollution
  const pollutionPercentage = distribution.dirty / samples.length;

  // Return `Clean` or `Polluted`
  return pollutionPercentage <= threshold ? "Clean" : "Polluted";
};
```
