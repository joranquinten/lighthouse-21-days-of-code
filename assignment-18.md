# Challenge #18 - In It to Win It ([link](https://coding-challenge.lighthouselabs.ca/challenge/18))

There are a number of different stands and games at this year's festival where the townspeople of Codeville can win raffle tickets! There are three different kinds of tickets someone can win, and they each correspond to a raffle. There are `red` tickets for the Red Robin Raffle, `green` tickets for the Green Machine Raffle and `blue` tickets for the Deep Blue Sea Raffle. The people of Codeville **love** games and always end up with a large number of tickets. So this year, we'll build a machine that not only sorts and counts the number of each ticket, but also tells people which raffle they have the best odds of winning based on the current entries.

## Instructions

Our first function, `bestOdds()`, will receive two parameters. The first parameter will be an array of strings that are either `red`, `green`, or `blue`, representing the tickets that a particular person has. The second parameter is an object that shows how many entries there currently are for each raffle. By looking at the tickets that the particular person has, your function should return a string that lets the person know which raffle they have the highest chance of winning. The format of the response should be as follows (without the square brackets): `"You have the best odds of winning the [COLOUR] raffle."`

While we could do this all within the `bestOdds()` function, we want to keep our code [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself), so we will also need to complete a helper function. This helper function `countTickets()` will be called from within `bestOdds()` and receive the array of strings that are either `red`, `green`, or `blue`. The function will count how many of each string there are, and then return an object with the individual counts.

## Examples

Input:

```js
// for bestOdds() function
const tickets = ["red", "red", "green", "blue", "green"];

const raffleEntries = {
  red: 10,
  green: 30,
  blue: 15
};
```

Output:

```js
"You have the best odds of winning the red raffle.";
```

Input:

```js
// for countVotes() helper function
const tickets = ["red", "red", "green", "blue", "green"];
```

Output:

```js
{
  red: 2,
  green: 2,
  blue: 1
}
```

## Resolution:

This makes for an interesting challenge, because we can solve this in a multitude of ways. I've built the solution to scale well with any extra colors in the future, because I make use of the dynamic linking capabilities in JavaScript.

First, the `countTickets()` function. What I want is an object where I can store all additions of the occurences in the array. Since the names in the array are identical to the property names in the object, I can use the dynamic addressing of object properties using the `[]` notation. To iterate over the array and at the same time construct the return object I make use of the `.reduce` function (again!). It starts with the empty object definition (`{ red: 0, green: 0, blue: 0}`) and for every entry in the `tickets` array, I use the spread operator (`...`) to return the object, but modify one entry, namely the current color. For the `return { ...total, [ticket]: total[ticket] + 1 };` part, it basically means: _"Return the `total` object and all of its values, but for the property that matches the value of `ticket` I want to modify it: give me the current value (`total[ticket`]) and add 1 to the current value."_
Because of the dynamically addressing of properties, I've wrapped it in a `try {} catch (e) {}` statement to be safe. That means that if the property was non existent, the `.reduce` will still return the `total` for the next iteration of the function.

```js
const countTickets = (tickets = []) => {
  return tickets.reduce(
    (total, ticket) => {
      try {
        return { ...total, [ticket]: total[ticket] + 1 };
      } catch (e) {
        return total;
      }
      return newTotal;
    },
    { red: 0, green: 0, blue: 0 }
  );
};
```

For the `bestOdds()`, I chose to do some other form of iteration. I store the output of the `countTickets()` function in the `ticketsCount` variable. This is an object which holds the ticket count per color. To match this with the raffleEntries I convert the `raffleEntries` **object** to its **keys** by using the `Object.keys()` method. Then, for every key (`red`, `green` and `blue`) I can match it to the `ticketsCount`, since they have matching property names. There's one layer I added on top of it, and that's used for determining the highest odds: I log the odds per color in an array that I construct using the `.reduce` function on the `Object.keys` array. This has an output that might look like:

```js
// Example of oddsPerColor
[
  { color: "green", odds: 0 },
  { color: "blue", odds: 0.02 },
  { color: "red", odds: 0.25 }
];
```

By using a `.sort()` function I compare, for every `object` in the `oddsPerColor` array, the `odds` attribute of said object. For said object, the sorted array would look like this:

```js
// Example of oddsPerColor.sort((a,b) => b.odds - a.odds)
[
  { color: "red", odds: 0.25 },
  { color: "blue", odds: 0.02 },
  { color: "green", odds: 0 }
];
```

Now I can be sure that the first entry of the array has the highest odds. So I address that with the _index_ of `[0]` and immediately return the `color` attribute, since thats the name I want to use in the return string.

```js
const bestOdds = (tickets = [], raffleEntries = {}) => {
  const ticketsCount = countTickets(tickets);

  const oddsPerColor = Object.keys(raffleEntries).reduce((total, color) => {
    return [
      ...total,
      { color: color, odds: ticketsCount[color] / raffleEntries[color] }
    ];
  }, []);

  const bestColor = oddsPerColor.sort((a, b) => b.odds - a.odds)[0].color;

  return `You have the best odds of winning the ${bestColor} raffle.`;
};
```
