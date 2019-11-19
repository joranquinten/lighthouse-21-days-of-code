# Challenge #19 - Pumpkin Spice and Everything Nice ([link](https://coding-challenge.lighthouselabs.ca/challenge/19))

This is the Codeville Fall Festival, and nothing says fall more than pumpkin spice. At this year's festival, there will be three ways for the people of Codeville to get their pumpkin spice fix:

1. Pumpkin pie
2. Pumpkin spice lattes
3. Pumpkin spice macarons

## Instructions

Each item differs in both cost and the grams of pumpkin spice per serving. To help festival-goers maximize their pumpkin spice consumption, help them determine the maximum amount of pumpkin spice they can ingest with the amount of money they are bringing to the festival.

- A slice of pumpkin pie costs \$5 each, and include a whopping 30g of pumpkin spice
- Pumpkin spice lattes cost \$3 each, and include 15g of pumpkin spice
- Pumpkin spice macarons cost \$1 each, and include 3g of pumpkin spice

We need to write a function, `pumpkinSpice(money)` that will take in a number, or how much the festival-goer has to spend on treats, and return an array with the 4 elements as outlined below:

- The first element should represent how many slices of pumpkin pie the client can buy
- The second element should represent how many pumpkin spice lattes the client can buy
- The third element should represent how many pumpkin spice macarons the client can buy
- The fourth element should represent how many grams of pumpkin spice the client will be buying

Our function should start by calculating how many slices of pumpkin pie we can buy. Then, we'll want to use the remaining money to do the calculations for the lattes, followed lastly by the macarons.

## Examples

Input:

```js
const money = 9;
```

Output:

```js
[1, 1, 1, 48];
```

# Resolution:

So, for this assignment, we're doing divisions with remainders. For this, we can use the modulus operater we've used on [day #16](assignment-16.md). We need to take in the money that a customer has, and traverse the products to see how much of the products they can buy, starting with the most expensive to the cheapest. (Fortunately, we don't have to factor in the best money to spice ratio). We can store the products in an object, which holds the amount of grams and selling price, because we need those for out math!

Then we can `.reduce` over the objects, take in the money available and construct the return array. Let's get to it:

```js
const pumpkinSpice = money => {
  // This is the object that holds the variables per product
  const products = [
    {
      price: 5,
      grams: 30
    },
    {
      price: 3,
      grams: 15
    },
    {
      price: 1,
      grams: 3
    }
  ];

  // We're going to store and update the remaining money in a variable
  let remainingMoney = money;

  return products.reduce(
    (output, product, index) => {
      const currentSpiceAmount = output[output.length - 1]; // Get the current amount of spice grams

      const amountOfProducts = Math.floor(remainingMoney / product.price); // Calculate the number of products that can be bought (and round down)
      const amountSpiceGrams = amountOfProducts * product.grams; // Multiply the amount of products that can be bought by the amount of grams per product

      remainingMoney = remainingMoney - amountOfProducts * product.price; // Update the remainingMoney
      output[index] = amountOfProducts; // Set the amount of products on the current index
      output[output.length - 1] = currentSpiceAmount + amountSpiceGrams; // Calculate the amount of grams and store it on the last position of the return array
      return output;
    },
    [0, 0, 0, 0] // The output to start out with
  );
};
```
