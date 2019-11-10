# Challenge #10 - SmartParking

The parking lot in the Codeville Devtropolis Shopping Mall needs an upgrade, and you've decided this is the perfect opportunity to install a smart parking system.

The system will use special parking sensors to keep track of all parking spots and monitor which ones are available. Every time a vehicle enters the parking lot, the system directs them to an available spot for their particular vehicle type, or notifies them that no spots are available.

## Instructions

We need to write a function called `whereCanIPark()` that returns the coordinates of an available parking spot for the vehicle, or returns false if there is no available spot. Our function receives an array of arrays representing parking spots, and a string with type of the vehicle that is looking for a parking spot.

There are three kinds of possible vehicles: **regular** cars, **small** cars, and **motorcycles**. Regular cars can only park in **R** spots. Small cars can park in **R** or **S** spots. Motorcycles can park in **R**, **S**, or **M** spots. In the array of parking spots, spots are written in both lower-case and upper-case. An upper-case letter means that the particular spot is **AVAILABLE**, while lower-case letters mean that the spot is **UNAVAILABLE**.

Our function must return an array with the coordinates of the spot as an [X, Y] pair. See the example input and output below for an illustration.

**Note**: There may be multiple available spots for a particular vehicle. It does not matter which spot your function chooses, as long as the spot is available. And if there are no available spots, remember to return false.

## Examples

Input:

```js
const spots = [
  // COLUMNS ARE X
  //    0    1    2    3    4    5
  ["s", "s", "s", "S", "R", "M"], // 0 ROWS ARE Y
  ["s", "M", "s", "S", "R", "M"], // 1
  ["s", "M", "s", "S", "R", "m"], // 2
  ["S", "r", "s", "m", "R", "M"], // 3
  ["S", "r", "s", "m", "R", "M"], // 4
  ["S", "r", "S", "M", "M", "S"] // 5
];

const vehicle = "regular"; // possible options are 'regular', 'small', or 'motorcycle'
```

Output:

```js
[4, 0];
```

## Resolution

A lot of reading, and a bit more complexity, since we're going to traverse a two dimensional array (or nested array).
For every spot, we need to do some checks, so I've abstracted that out to a separate function (`isAvailable`), for readability of the function.

By default, the return value (`coords`) is assumed to be false. The first occurence will set the variable, which then can be returned.

The return value should be first the row, then the column (which is kind of odd).

```js
const whereCanIPark = (spots, vehicle) => {
  const isAvailable = (spot, vehicle) => {
    if (vehicle === "small") {
      return spot === "R" || spot === "S";
    }
    if (vehicle === "regular") {
      return spot === "R";
    }
    if (vehicle === "motorcycle") {
      return spot === "S" || spot === "R" || spot === "M";
    }
  };

  let coords = false;
  spots.forEach((column, colIndex) => {
    column.forEach((spot, rowIndex) => {
      if (!coords && isAvailable(spot, vehicle)) {
        coords = [rowIndex, colIndex];
      }
    });
  });

  return coords;
};
```
