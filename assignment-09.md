# Challenge #9 - Driving Mayor Daisy ([link](https://coding-challenge.lighthouselabs.ca/challenge/9))

As Mayor, you want one of your legacies to be bettering street design enough to improve traffic flow and reduce congestion. You've decided to start by installing special sensors on some streets to monitor how often cars pass by, and track their speeds.

## Instructions

Complete the function, `carPassing(cars, speed)`, that takes in an array of car objects, and the speed of a car as it passes the sensor. This function should create a new object with with a property called speed, and another property called time and add it to the cars array. We can retrieve the current time, for setting the `time` property, by using the `Date.now()` function, which is built into JavaScript!

Our function should return an array that includes all of the elements in cars as well as our new element.

## Examples

Input:

```js
const cars = [
  {
    time: 1568329654807,
    speed: 40
  },
  {
    time: 1568329821632,
    speed: 42
  },
  {
    time: 1568331115463,
    speed: 35
  }
];

const speed = 38;
```

Output:

```js
[
  {
    time: 1568329654807,
    speed: 40
  },
  {
    time: 1568329821632,
    speed: 42
  },
  {
    time: 1568331115463,
    speed: 35
  },
  {
    time: 1568431216417,
    speed: 38
  }
];
```

## Resolution:

This function draws on the strength of the array spread operator (`...`). In this case, it spreads the original array into the return array, then adds the new requested object. We also use a shorthand for passing the speed. When constructing objects, the notation of an attribute with the same variable name `{ speed: speed }` can be simply abbreviated to `{ speed }`.

```js
const carPassing = (cars = [], speed = 0) => {
  return [...cars, { time: Date.now(), speed }];
};
```
