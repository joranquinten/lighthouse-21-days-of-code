# Challenge #20 - Bouncy Castles ([link](https://coding-challenge.lighthouselabs.ca/challenge/20))

There's a new attraction at this year's town festival. The organizers have decided to bring in several inflatable attractions, but they have no clue how to much blow them up. Each attraction needs to be pumped to a precise volume to achieve maximum festival fun!

The attractions are each made up of a combination of several different shapes: cones, spheres and prisms. For example, the giant inflatable duck is made up of two spheres (the body and head) and a cone (the beak) 🦆.

## Instructions

Each shape has a different calculation for determining volume, so we'll need to create a few functions that will help us figure out the volume of the various inflatable attractions.

In this challenge, we'll need to implement four functions.

The first three will calculate the volume of the individual shapes:

- `sphereVolume()` will calculate the volume of a sphere given a radius
- `coneVolume()` will calculate the volume of a cone given a radius and a height
- `prismVolume()` will calculate the volume of a prism given a height, a width, and a depth

The fourth function, `totalVolume()`, will receive an array containing the different shapes that make up a single attraction. The totalVolume function should use the previous three functions to calculate the total volume of an attraction.

Don't worry about getting the answers to the perfect precision: our tests will check to see that you're within a correct range.

## Examples

Input:

```js
const sphere = {
  type: "sphere",
  radius: 2
};

sphereVolume(sphere.radius);
```

Output:

```js
33.5102;
```

Input:

```js
const cone = {
  type: "cone",
  radius: 3,
  height: 5
};

coneVolume(cone.radius, cone.height);
```

Output:

```js
47.12385;
```

Input:

```js
const prism = {
  type: "prism",
  height: 3,
  width: 4,
  depth: 5
};

coneVolume(prism.height, prism.width, prism.depth);
```

Output:

```js
60;
```

Input:

```js
const largeSphere = {
  type: "sphere",
  radius: 40
};

const smallSphere = {
  type: "sphere",
  radius: 10
};

const cone = {
  type: "cone",
  radius: 3,
  height: 5
};

const duck = [largeSphere, smallSphere, cone];

totalVolume(duck);
```

Output:

```js
49.8;
```

## Resolution:

The most work is looking up the functions to calculate volume (since my Math days are long gone). Once I had those, the challenge is fairly straightforward. We use a `.reduce` function to map over the shapes we're receiving in the `totalVolume()` function. For every shape we take in the `type` and based on the type we know which function to call (and pass variables to) in order to get the volumne.

Instead of using the provided `PI` value, I just used the `Math.PI` constant that's built into JavaScript.

```js
const sphereVolume = function(radius = 0) {
  return (4 / 3) * Math.PI * Math.pow(radius, 3);
};

const coneVolume = function(radius = 0, height = 0) {
  return (Math.PI * radius * radius * height) / 3;
};

const prismVolume = function(height = 0, width = 0, depth = 0) {
  return height * width * depth;
};

const totalVolume = function(solids = []) {
  return solids.reduce((totalVolume, shape) => {
    let addVolume = 0;
    if (shape.type === "sphere") {
      addVolume = sphereVolume(shape.radius);
    }
    if (shape.type === "cone") {
      addVolume = coneVolume(shape.radius, shape.height);
    }
    if (shape.type === "prism") {
      addVolume = prismVolume(shape.height, shape.width, shape.depth);
    }
    return totalVolume + addVolume;
  }, 0);
};
```
