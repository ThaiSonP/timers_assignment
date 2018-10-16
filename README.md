# Rock, Paper, Scissors

You tried in the JavaScript workshop, but you were missing one crucial element: *callbacks*.

Take a look at this:

```js
const readline = require('readline');

const reader = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

reader.question(`sup? \n`, (res) => {
  console.log(`you replied: ${res}`)
});
```

`readline` is what's known as a *library*. Don't worry about what that is, precisely, yet - just know that, like class methods, it's something that Node makes available to us to use how we'd like.

You can see here that we're using callbacks to *await a user's response*. The first argument of `question` prints to the console to ask a question, and the second is a callback which handles what our user might say. Once we have that response, our callback fires and we tell them what they wrote.

Using this library, we are going to make a rock, paper, scissors game against the computer. Our finished product should converse something like this:

```
Console: `Welcome to rock, paper, scissors. Please type 'r', 'p', or 's' to make a choice.`
User: `rock`
Console: `You chose 'rock'. Hmm...` (setTimeout for 5 seconds here to imagine the computer thinking)
Console: `The computer chose 'scissors'.`
Console: `Congratulations! You win!`
```

...And then the program exits.

A few notes here:

* Use the full extent of the [readline library](https://node.readthedocs.io/en/latest/api/readline/) to flesh out your program's functionality.
* The computer should make a random choice (`Math.random` might be useful here) to come up with their play.
* You should handle wins, losses, and ties.


const readlineSync = require('readline-sync');

console.log("Welcome to rock, paper, scissors. Please type 'r', 'p', or 's' to make a choice.?");

readlineSync.promptLoop(function(input) {

  let userRes = input;
  let computerRes = "";


  if(Math.floor(Math.random()* 3) === 1){
    computerRes = "r"
  }else if(Math.floor(Math.random()* 3) === 2){
    computerRes = "p"
  }else {
    computerRes = "s"
  }

  let msg = "";

  if(userRes === computerRes){
    msg = "Sorry you tied, try again";
  } else if((computerRes === "r" && userRes === "p") ||
            (computerRes === 'p' && userRes === 's') ||
            (computerRes === 's' && userRes === 'r')){
      msg = "You win (for now), whatever. Computers are gonna win in the end";
  } else {
      msg = "You lose!!! You big loser!!!";
  }
    console.log(msg);

  return msg === "You win (for now), whatever. Computers are gonna win in the end";
});


## Bonus

[Eliza](http://psych.fullerton.edu/mbirnbaum/psych101/Eliza.htm) is one of the world's first chatbots. She uses the user's response to come up with a question, mimicking a not-so-insightful therapist. She never says anything herself - she simply picks a detail the user wrote and asks a new question. Play around with her in the link above and see how this works.

Your task is to use `readline` to **write a simple version of Eliza** - a chatbot that can handle any input and return an at-least-sort-of-relevant question.

*Hint*: When the user says "I" or "I'm" or any word referring to themselves, that's a dead giveaway that the next thing they write will be useful to your response.
