# Challenge #16 - In Living Colour ([link](https://coding-challenge.lighthouselabs.ca/challenge/16))

It's time to order the banners and flags for the festival, and you need to decide on the key colour scheme.

You want to use colour theory to make sure the colours complement one another. To do so we'll need to choose a main colour and use code to determine the best complementary colours.

## Instructions

We'll complete a function `festivalColours()` that calculates the [split complementary colours](https://www.w3schools.com/colors/colors_compound.asp) for a given colour. We'll be working with a special colour system called HSL, which stands for Hue, Saturation, and Lightness.

[Here's an example of an HSL colour picker.](http://hslpicker.com/)

The function will receive an `H(Hue)` value, and must return an array of the values for the two split complementary colours. The smaller number should be the first element, and the larger number should be the second element.

You can take a peek at [this website](https://www.ethangardner.com/articles/2009/03/15/a-math-based-approach-to-color-theory-using-hue-saturation-and-brightness-hsb/#split-complementary) for the formula you'll need to use to calculate the split complementary colours.

## Examples

Input:

```js
const color1 = 100;
```

Output:

```js
[250, 310];
```

## Resolution:

The resolution is fairly simple, once you've found the formula. It basically says that based on the first color value, you have to add respectively 150 and 210 to that base. The only thing you have to worry about, is that you're calculating _degrees on a circle_ which means there are not valid values above 360. To make sure we return only valid colors, we can see if the result is bigger than 360 and then subtract until the value is below, but we can also use the [modulus operator](https://www.w3schools.com/js/js_arithmetic.asp) to get the remainder of a division.

```js
const festivalColours = color1 => {
  const colorMod = (base, value) => ((base + value) % 360);

  return [colorMod(color1, 150), colorMod(color1, 210)];
}
};
```
