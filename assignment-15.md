# Challenge #15 - X Marks the Perfect Shot 📸 ([link](https://coding-challenge.lighthouselabs.ca/challenge/15))

With the city getting smarter, it's time to turn your focus to Codeville's biggest event of the year, the Harvest Festival! Each year, the Harvest Festival kicks off with a parade - and you want to make sure this is a show the townspeople will remember forever.

You've hired Daria Ducksworth, the town's best photographer, to capture the magic of the Harvest Festival Parade. She needs to track the coordinates of the floats to help her capture their best angles.

## Instructions

For this challenge you'll have to implement a function called `paradePosition()`, which will calculate the position of the parade based on an array of directional moves. The parade will move on an X-Y grid like the following.

![Visual representation of the grid](https://etc.usf.edu/clipart/49200/49288/49288_graph_0505b_md.gif)

Your function will receive an array of moves, which are strings that say either `north`, `south`, `west`, or `east`, these represent the parade moving in a particular direction by a single space on the grid. By looking at the path that the parade moves in, your function should calculate and then return an array representing the position of the parade after completing all of the moves. The first element of the array should be the X position, and the second element of the array should be the Y position. The parade begins at `[0,0]`.

## Examples

Input:

```js
const moves = ["north", "north", "west", "west", "north", "east", "north"];
```

Output:

```js
[-1, 4];
```

## Resolution:

In order to solve this, you need to determine a couple of things:

- Based on de `move` you need to update either the X-axis or the Y-axis;
- Said axis needs to be updated with a `+1` or a `-1` value;
- Return the updated position

The complexity does not lie in updating, once you have the proper values. That's why I focussed on optimizing the first two steps. I've stored the output of the move (value and axis) in an `object`. In order to reference the correct values, I've stored them in a `directionMap` where the attribute name matches one of the possible values in the `moves` array.

I proceed to iterate over the `moves` array and for each move, the function, does the following:

- Get the properties from the `directionMap` (for instance: `directionMap['west']` would reference the `west` property);
- The property is [destructed](https://developer.mozilla.org/nl/docs/Web/JavaScript/Reference/Operatoren/Destructuring_assignment), which is basically a shorthand of saying: `const index = directionMap[move].index`;
- After getting the values, it's a simple matter of updating the `position` array on the correct axis (`index`) with the correct mutation (`+= value`) and returning it ✌️

```js
const finalPosition = (moves = []) => {
  const directionMap = {
    west: {
      value: -1,
      index: 0
    },
    east: {
      value: 1,
      index: 0
    },
    south: {
      value: -1,
      index: 1
    },
    north: {
      value: 1,
      index: 1
    }
  };

  let position = [0, 0];

  moves.forEach(move => {
    const { index, value } = directionMap[move];
    position[index] = position[index] += value;
  });
  return position;
};
```
