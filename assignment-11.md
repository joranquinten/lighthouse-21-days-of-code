# Challenge #11 - You Can't Hurry Transit ([link](https://coding-challenge.lighthouselabs.ca/challenge/11))

You can't hurry love, or local transit in Codeville. While you've been hard at work on a solution to the larger transit woes, you've decided to implement a new system to at least be a little more transparent about wait times. The city will be installing a smart screen, at the busiest bus stop in town, that will show the estimated arrival times for each of the buses that stop there.

## Instructions

For this challenge, we'll implement a function called `busTimes()`. This function will calculate the arrival time for a collection of busses based on their current speed and distance from the stop. It will receive an object called `buses`, which contains a series of objects for each bus, with the distance of the bus and the speed that the bus is traveling at. Our function should return a new object that shows how long until each bus arrives at the stop.

## Examples

Input:

```js
const buses = {
  pickadilly: {
    distance: 10,
    speed: 5
  },
  uptown: {
    distance: 13,
    speed: 10
  }
};
```

Output:

```js
    {
      pickadilly: 2,
      uptown: 1.3
    }
```

## Resolution:

This challenge allows for some dynamic parsing of the object structure. If we assume more destinations might be added, we can accomodate for future events by traversing the object keys with the appropiately named `Object.keys()` method. We then use a `.reduce()` method to build up the expected resulting object.
With more dynamic input, it makes sense to wrap a `try` `catch()` around it, so the code doesn't break when something unexpected gets passed to the function.

```js
const busTimes = buses => {
  return Object.keys(buses).reduce((times, key) => {
    try {
      times[key] = buses[key].distance / buses[key].speed;
    } catch (e) {
      console.error(`Not possible to process ${key}`, e);
    }
    return times;
  }, {});
};
```
