# Challenge #1 - Door to Door ([link](https://coding-challenge.lighthouselabs.ca/challenge/1))

Our challenge begins in Codeville, a small but thriving town in Serverside, Canada, where you are the current mayor nearing the end of your first term. Election season is nearing, and this town needs you, so you've decided to run for a second term. However, you need some help to make sure the election and your campaign run smoothly. Enter JavaScript, a coding language sure to help you optimize the many elements of the upcoming election and (hopefully) secure your return as Mayor.

As your election campaign ramps up, you plan to go door to door to talk to the citizens of Codeville. There are quite a few neighbourhoods in Codeville, but lucky for you, we have a dedicated crew of volunteers to help out. Being the fair Mayor that you are, you want to make sure the work is distributed evenly between the team. Let's figure out how many neighbourhoods each volunteer should visit.

## Instructions

Given an array of volunteer names and an array of neighbourhood names, complete the doorToDoor function so that it returns the number of neighbourhoods each volunteer should visit if the work of going door to door is split evenly amongst them.

## Examples

Input:

```js
const volunteers = ["Sally", "Jake", "Brian", "Hamid"];

const neighbourhoods = [
  "Central Valley",
  "Big Mountain",
  "Little Bridge",
  "Bricktown",
  "Brownsville",
  "Paul's Boutique",
  "Clay Park",
  "Fox Nest"
];
```

Output:

```js
2;
```

## Resolution:

Simple division of the two variables. The `(neighbourhoods = ['one'])` part makes sure we don't divide by zero, when no variable is provided.

```js
const doorToDoor = (volunteers = [], neighbourhoods = ["one"]) => {
  return Math.floor(neighbourhoods.length / volunteers.length);
};
```
