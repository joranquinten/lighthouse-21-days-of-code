# Challenge #13 - All of the Lights

To make late-night driving and walking safer(and to save the city energy), you've decided to install smart street lights. These lights turn on and off automatically when they sense someone near by.

You'll need to use JavaScript to create some of the functionality to control the lights.

##3 Instructions
We will be implementing this using three functions.

The first two functions will receive an array of objects that represent street lights which may be `on` or `off`.

- Our first function, `lightsOn`, must set all of the lights to on and then return the array of lights.
- The second function, `lightsOff`, must set all the lights to "off" and then return the array of lights.
- The third function, `toggleLights`, will receive an array of many street lights, as well as a boolean value `lightsAreOn` which tells you whether or not all the lights are currently on. If `lightsAreOn` is true, your function should turn all of the lights off. If `lightsAreOn` is false, your function should turn all of the lights on.

## Examples

Input:

```js
// for lightsOff() function
const lights = [
  {
    id: 1,
    on: true
  },
  {
    id: 2,
    on: true
  },
  {
    id: 3,
    on: true
  },
  {
    id: 4,
    on: true
  },
  {
    id: 5,
    on: true
  }
];
```

Output:

```js
[
      {
          id: 1,
          on: false
      },
      {
          id: 2,
          on: false
      },
      {
          id: 3,
          on: false
      },
      {
          id: 4,
          on: false
      },
      {
          id: 5,
          on: false
      }
    ],
```

Input:

```js
// for lightsOn() function
const lights = [
  {
    id: 1,
    on: false
  },
  {
    id: 2,
    on: false
  },
  {
    id: 3,
    on: false
  },
  {
    id: 4,
    on: false
  },
  {
    id: 5,
    on: false
  }
];
```

Output:

```js
[
  {
    id: 1,
    on: true
  },
  {
    id: 2,
    on: true
  },
  {
    id: 3,
    on: true
  },
  {
    id: 4,
    on: true
  },
  {
    id: 5,
    on: true
  }
];
```

Input:

```js
// for toggleLights() function
const lights = [
  {
    id: 1,
    on: true
  },
  {
    id: 2,
    on: true
  },
  {
    id: 3,
    on: true
  },
  {
    id: 4,
    on: true
  },
  {
    id: 5,
    on: true
  }
];

const lightsAreOn = true;
```

Output:

```js
[
  {
    id: 1,
    on: false
  },
  {
    id: 2,
    on: false
  },
  {
    id: 3,
    on: false
  },
  {
    id: 4,
    on: false
  },
  {
    id: 5,
    on: false
  }
];
```

## Resolution:

This assignment has a lot of examples, but is actually fairly simple. Bear in mind that the functions you create to turn the lights `on` or `off`, you can reuse to fulfill the `toggleLights` requirement.

The `lightsOn` and `lightsOff` function both work similarly: we `.map` the array to get a handle on each of the items in the array. We use the _spread operator_ (`...`) to make a shallow clone of the original item. This way we can copy the original properties, by providing de `on` or `off` property manually, we basically say: 'Copy the existing object, but replace this property with the given value'.

The output is an array where all `on` properties have received the requested value.

The `toggleLights` simply takes in the `lights` and `lightsAreOn` array. It uses a ternary operator to choose whether lights should be turned `off` or `on` and immediately return the output of those functions.

```js
const lightsOn = function(lights = []) {
  return lights.map(light => ({ ...light, on: true }));
};

const lightsOff = function(lights = []) {
  return lights.map(light => ({ ...light, on: false }));
};

const toggleLights = function(lights = [], lightsAreOn = false) {
  return lightsAreOn ? lightsOff(lights) : lightsOn(lights);
};
```
