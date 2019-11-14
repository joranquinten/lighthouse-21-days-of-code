# Challenge #8 - Trash to Treasure ([link](https://coding-challenge.lighthouselabs.ca/challenge/8))

The results are in, and the people of Codeville want you to focus on Smart City upgrades. You've decided to begin by replacing all of the city's trash cans with smart cans: when citizens toss their rubbish into the smart can, it automatically sorts items into waste, recycling, and compost bins.

## Instructions

We need to complete a function called `smartGarbage(trash, bins)`, which will be responsible for increasing the garbage count for waste, recycling, or compost depending on what trash is submitted. Our function will receive two arguments. The first argument, `trash`, is a string that will tell our function what type of item is being submitted. The second argument, `bins`, is an object containing three properties (`waste`, `recycling`, and `compost`), which hold some numerical value. Our function must increase the correct value in the `bins` object, and the return the newly updated object.

## Examples

Input:

```js
const bins = {
  waste: 4,
  recycling: 2,
  compost: 5
};

const trash = "recycling";
```

Output:

```js
{
    waste: 4,
    recycling: 3,
    compost: 5
}
```

## Resolution:

Using object spreading, this assigment can be fulfilled rather easily. But since it can break when the values are not as expected, I've wrapped the return in a `try` ... `catch` statement, and simply return the `bins` when an error occurs.

```js
const smartGarbage = (trash, bins) => {
  try {
    return { ...bins, [trash]: bins[trash] + 1 };
  } catch (e) {
    return bins;
  }
};
```
