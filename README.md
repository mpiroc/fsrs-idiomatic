## About The Project

fsrs.js is a JS Package implements [Free Spaced Repetition Scheduler algorithm](https://github.com/open-spaced-repetition/free-spaced-repetition-scheduler). It helps developers apply FSRS in their flashcard apps.

## Getting Started

```
npm install fsrs.js
```

## Usage

Create a card and review it at a given time:

```js
const fsrsJs = require("fsrs.js")

let fsrs = new fsrsJs.FSRS();
let card = new fsrsJs.Card();
let rating= fsrsJs.Rating;
let state = fsrsJs.State;

//Set algorithm parameters
// fsrs.p.request_retention=0.9
// fsrs.p.maximum_interval=36500
// fsrs.p.w=[0.4, 0.6, 2.4, 5.8, 4.93, 0.94, 0.86, 0.01, 1.49, 0.14, 0.94, 2.18, 0.05, 0.34, 1.26, 0.29, 2.61]

console.log(fsrs.p)

let now = new Date(2022, 10, 29, 12, 30, 0, 0);
let scheduling_cards = fsrs.repeat(card, now);
console.log(scheduling_cards);
```

There are four ratings:

```js
rating.Again //incorrect response
rating.Hard //recall; correct response recalled with serious difficulty
rating.Good //recall; correct response after a hesitation
rating.Easy // recall; perfect response
```

There are four states:

```js
state.New //Never been studied
state.Learning //Been studied for the first time recently
state.Review //Graduate from learning state
state.Relearning //Forgotten in review state
```

```js
//Get the new state of card for each rating:
scheduling_cards[rating.Again].card
scheduling_cards[rating.Hard].card
scheduling_cards[rating.Good].card
scheduling_cards[rating.Easy].card

//Update the card after rating `Good`:
card = scheduling_cards[rating.Good].card

//Get the due date for card:
due = card.due

//Get the state for card:
state = card.state

//Get the review log after rating `Good`:
review_log = scheduling_cards[rating.Good].review_log
```

## License

Distributed under the MIT License. See `LICENSE` for more information.
