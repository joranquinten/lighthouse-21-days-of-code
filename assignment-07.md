# Challenge #7 - You Choose, (You Don't) Lose

The people of Codeville have spoken, and you have been elected mayor once again! Now it's time to get back to work. You need to decide which issues to focus on first for your new term in office. Using the dataset from voter surveys, determine the top three issues voters were most concerned about when choosing the new Codeville leadership.

## Instructions

We need to go through the survey responses to see what your constituents would like you to focus on over the course of your term in office. The array that you are given contains many phrases and words pulled from a number of interviews. We only want to focus on the following three key phrases: "smart city", "arts funding", and "transportation".

Our `termTopics` function needs to count how many times each of those topics was mentioned in the surveys, and then return an array with the number of mentions in the following order: `smart city`, `arts funding`, and then `transportation`.

## Examples

Input:

```js
const interviews = [
  "smart city",
  "rebuild the lighthouse",
  "arts funding",
  "transportation",
  "arts funding",
  "rebuild the lighthouse",
  "sports funding",
  "tax cuts",
  "smart city",
  "arts funding",
  "smart city"
];
```

Output:

```js
[
  3, // smart city
  3, // arts funding
  1 // transportation
];
```

## Resolution:

Again, I use the `.reduce` function to process the input array and immediately construct the expected output. Since the output values are in a predefined order, we can tally on specific entries of the raturn array.

```js
const termTopics = (interviews = []) => {
  return interviews.reduce(
    (tally, topic) => {
      if (topic === "smart city") {
        tally[0] = tally[0] + 1;
      }
      if (topic === "arts funding") {
        tally[1] = tally[1] + 1;
      }
      if (topic === "transportation") {
        tally[2] = tally[2] + 1;
      }
      return tally;
    },
    [0, 0, 0]
  );
};
```
