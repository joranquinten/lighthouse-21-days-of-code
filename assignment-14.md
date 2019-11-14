# Challenge #14 - Ticket to Ride ([link](https://coding-challenge.lighthouselabs.ca/challenge/14))

The local transit system has been too expensive for too long! To encourage more people to use the bus, you are restructuring ticket pricing. From now on, passengers will be charged a dynamic price, which will depend on the number of people on the bus (peak times have higher fare!) and the distance that the passenger travels.

## Instructions

We'll be implementing a function called `dynamicPricing()`, which will return the cost of a particular trip given the number of people on the bus, and the distance traveled by the passenger. This function receives two numbers: `numberOfPeople` and `distanceTraveled`.

The base ticket price is $1. Passengers will be charged $0.25 per kilometer. If there are 30 or more people on the bus, there should be \$0.25 added to the total.

The value that your functions returns must be a string, formatted as such: \$4.25. Your values must be shown to two decimal points of precision.

## Examples

Input:

```js
const numberOfPeople = 15;
const distanceTraveled = 10;
```

Output:

```js
$3.50
```

Input:

```js
const numberOfPeople = 35;
const distanceTraveled = 5;
```

Output:

```js
$2.50
```

## Resolution:

For the most part, this assignment is pretty straigtforward. You have to return a price, which has a minimum and then factor in some rules for increasing the price. Not that complicated when you follow the text.

The return value is requested in a certain format thought, and that makes for an interesting use case, the [`Intl` object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NumberFormat#Specifications) can format pretty sturdy and it [gaining support](https://caniuse.com/#search=Intl) in all major browsers nowadays. The object also allows for hypothetical future requirements of supporting different currency formatters.

```js
const dynamicPricing = (numberOfPeople, distanceTraveled) => {
  let price = 1.0;

  price += distanceTraveled * 0.25;
  if (numberOfPeople >= 30) price += 0.25;

  const currencyFormatter = new Intl.NumberFormat("en-US", {
    style: "currency",
    currency: "USD"
  });

  return currencyFormatter.format(price);
};
```
