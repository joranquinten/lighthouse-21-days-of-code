# Challenge #2 - Something to Talk About ([link](https://coding-challenge.lighthouselabs.ca/challenge/2))

Thanks to your tireless volunteers, the word is out that you're running for a second term, and the local media has come calling!

The Lighthouse Gazette wants to interview you about your campaign, but you're a nervous interviewer! To help prepare for your interview you want to use JavaScript to practice campaign stance on important election topics. The list of possible question categories includes:

- arts funding
- economy
- transportation

## Instructions

Given a question topic, complete a function interviewAnswer(topic) that returns your stance on that particular election issue. The answer should be returned as a string.

When asked about arts funding, the function should return `"We'll have to get creative!"`
When asked about the economy, the function should return `"Time is money."`
When asked about transportation, the function should return `"It's going to be a long road, so we better get moving."`
If you're asked about a topic that isn't in the list above, respond with a default statement. (For example, "QUACK!")

## Examples

Input:

```js
const topic = "economy";
```

Output:

```js
"Time is money.";
```

Input:

```js
const topic = "transportation";
```

Output:

```js
"It's going to be a long road, so we better get moving.";
```

## Resolution:

A classic switch statement.

```js
const interviewAnswer = topic => {
  let response;
  switch (topic) {
    case "arts funding":
      response = "We'll have to get creative!";
      break;
    case "economy":
      response = "Time is money.";
      break;
    case "transportation":
      response = "It's going to be a long road, so we better get moving.";
      break;
    default:
      response = "QUACK!";
      break;
  }

  return response;
};
```
