#### HTML

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta http-equiv="X-UA-Compatible" content="ie=edge" />
  <link rel="stylesheet" href="style.css" />
  <title>Guess My Number!</title>
</head>

<body>
  <header>
    <h1>Guess My Number!</h1>
    <p class="between">(Between 1 and 20)</p>
    <button class="btn again">Again!</button>
    <div class="number">?</div>
  </header>
  <main>
    <section class="left">
      <input type="number" class="guess" />
      <button class="btn check">Check!</button>
    </section>
    <section class="right">
      <p class="message">Start guessing...</p>
      <p class="label-score">💯 Score: <span class="score">20</span></p>
      <p class="label-highscore">
        🥇 Highscore: <span class="highscore">0</span>
      </p>
    </section>
  </main>
  <script src="script.js"></script>
</body>

</html>
```

#### JS

```js
'use strict';

// set secret number
const secretNumberResetter = function () {
  return Math.trunc(Math.random() * 20) + 1;
};

let secretNumber = secretNumberResetter();
let score = 20;
let highScore = 0;

const displayMessage = function (message) {
  document.querySelector('.message').textContent = message;
};

const scoreMessage = function (message) {
  document.querySelector('.score').textContent = message;
};

// when guess is correct (WIN SCENARION)
const winScenario = function () {
  displayMessage('🎉 Correct Number');
  document.querySelector('body').style.backgroundColor = '#60b347';
  document.querySelector('.number').style.width = '30rem';
  document.querySelector('.number').textContent = secretNumber;
  if (highScore < score) {
    highScore = score;
    document.querySelector('.highscore').textContent = highScore;
  }
};

// When guess is incorrect (Check loss!)
const wrongAnswer = function (guess) {
  if (score > 1) {
    displayMessage(guess > secretNumber ? '📈 Too high!' : '📉 Too low!');
    score--;
    scoreMessage(score);
  } else {
    scoreMessage(0);
    displayMessage('😭 You lost the game!');
  }
};

const resetGame = function () {
  // reset score
  score = 20;
  scoreMessage(score);

  // reset secret number
  secretNumber = secretNumberResetter();
  document.querySelector('.number').textContent = '?';

  // reset guess input
  document.querySelector('.guess').value = '';

  // reset gui
  displayMessage('Start guessing...');
  document.querySelector('body').style.backgroundColor = '#222';
  document.querySelector('.number').style.width = '15rem';
};

// ---------------- CORE GAME LOGIC BELOW ----------------//

// game logic
document.querySelector('.check').addEventListener('click', function () {
  const guess = Number(document.querySelector('.guess').value);
  // When there is no input
  if (!guess) {
    displayMessage('⛔ No number!');
  }

  // When player wins
  if (guess === secretNumber) {
    winScenario();
  } else if (guess !== secretNumber) {
    wrongAnswer(guess);
  }
});

document.querySelector('.again').addEventListener('click', function () {
  resetGame();
});
```

#### CSS

```css
@import url('https://fonts.googleapis.com/css?family=Press+Start+2P&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

html {
  font-size: 62.5%;
  box-sizing: border-box;
}

body {
  font-family: 'Press Start 2P', sans-serif;
  color: #eee;
  background-color: #222;
  /* background-color: #60b347; */
}

/* LAYOUT */
header {
  position: relative;
  height: 35vh;
  border-bottom: 7px solid #eee;
}

main {
  height: 65vh;
  color: #eee;
  display: flex;
  align-items: center;
  justify-content: space-around;
}

.left {
  width: 52rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.right {
  width: 52rem;
  font-size: 2rem;
}

/* ELEMENTS STYLE */
h1 {
  font-size: 4rem;
  text-align: center;
  position: absolute;
  width: 100%;
  top: 52%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.number {
  background: #eee;
  color: #333;
  font-size: 6rem;
  width: 15rem;
  padding: 3rem 0rem;
  text-align: center;
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translate(-50%, 50%);
}

.between {
  font-size: 1.4rem;
  position: absolute;
  top: 2rem;
  right: 2rem;
}

.again {
  position: absolute;
  top: 2rem;
  left: 2rem;
}

.guess {
  background: none;
  border: 4px solid #eee;
  font-family: inherit;
  color: inherit;
  font-size: 5rem;
  padding: 2.5rem;
  width: 25rem;
  text-align: center;
  display: block;
  margin-bottom: 3rem;
}

.btn {
  border: none;
  background-color: #eee;
  color: #222;
  font-size: 2rem;
  font-family: inherit;
  padding: 2rem 3rem;
  cursor: pointer;
}

.btn:hover {
  background-color: #ccc;
}

.message {
  margin-bottom: 8rem;
  height: 3rem;
}

.label-score {
  margin-bottom: 2rem;
}

```

