# Challenge #6 - Turn Out For What

Phew, with our help the city staff were able to select the voting stations on time and the election went off without a hitch! Now that the votes have been cast, the Election staff needs to verify the votes by matching each voter's signature to their voter ID.

## Instructions

Complete the function `voterTurnout()`, that will take in two arrays. The first array is a list of voter ids, and the second array is a list of voter signatures, which correspond to the voter ids. Our task here is to first check that each array have the same number of items and then confirm that each of the voter ids matches the corresponding voter signature.

If the arrays do not contain the same number of items, then we know something is amiss and our function should return false. If they contain the same number of elements, then we should proceed to check if the two arrays are identical, meaning they contain the same names in the same order. If they are, our function should return "All clear, we can count the votes!", if they are not it should return "FRAUD!".

## Examples

Input:

```js
const voter_signatures = [
  "Bill Billiamson",
  "Kate Etak",
  "Brandon Brandonus",
  "Fake McFakerson",
  "Jane Janesford"
];

const voter_ids = [
  "Bill Billiamson",
  "Kate Etak",
  "Brandon Brandonus",
  "Simon Simonson",
  "Jane Janesford"
];
```

Output:

```js
"FRAUD!";
```

Input:

```js
const voter_signatures = [
  "Bill Billiamson",
  "Kate Etak",
  "Brandon Brandonus",
  "Simon Simonson",
  "Jane Janesford"
];

const voter_ids = [
  "Bill Billiamson",
  "Kate Etak",
  "Brandon Brandonus",
  "Simon Simonson",
  "Jane Janesford"
];
```

Output:

```js
"All clear, we can count the votes!";
```

## Resolution:

There's a caveat in the assigment, namely that you also need to verify that the **position** of the signature matches the idea. There are serveral ways of doing this (for instance, comparing the output of `.indexOf()` method on both arrays). I chose to simply loop through the array.

```js
const voterTurnout = (voter_signatures = [], voter_ids = []) => {
  if (voter_signatures.length !== voter_ids.length) return false;

  let response = "All clear, we can count the votes!";
  (voter_signatures || []).forEach((signature, index) => {
    if (voter_ids[index] !== signature) response = "FRAUD!";
  });
  return response;
};
```
