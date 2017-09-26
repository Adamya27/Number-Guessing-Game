# Number-Guessing-Game
A client side simple game made using javascript


<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">

    <title>Number guessing game</title>

    <style>
      html {
        font-family: sans-serif;
      }
      body {
        width: 50%;
        max-width: 800px;
        min-width: 480px;
        margin: 0 auto;
      }
      .lastResult {
        color: white;
        padding: 3px;
      }
    </style>
  </head>

  <body>
      <h1>Number guessing game</h1>

      <p>We have selected a random number between 1 and 100. See if you can guess it in 10 turns or fewer. We'll tell you if your guess was too high or too low.</p>

<div class="form">
  <label for="guessField">Enter a guess: </label><input type="text" id="guessField" class="guessField">
  <input type="submit" value="Submit guess" class="guessSubmit">
</div>

<div class="resultParas">
  <p class="guesses"></p>
  <p class="lastResult"></p>
  <p class="lowOrHi"></p>
    <p class="guessrange"></p>
</div>

<script>
   // var rang = document.querySelector('.guessrange');
  var randomNumber = Math.floor(Math.random() * 100) + 1;

var guesses = document.querySelector('.guesses');
var lastResult = document.querySelector('.lastResult');
var lowOrHi = document.querySelector('.lowOrHi');

var guessSubmit = document.querySelector('.guessSubmit');
var guessField = document.querySelector('.guessField');

var guessCount = 1;
var resetButton;
    function resetGame() {
  guessCount = 1;

  var resetParas = document.querySelectorAll('.resultParas p');
  for (var i = 0 ; i < resetParas.length ; i++) {
    resetParas[i].textContent = '';
  }

  resetButton.parentNode.removeChild(resetButton);

  guessField.disabled = false;
  guessSubmit.disabled = false;
  guessField.value = '';
  guessField.focus();

  lastResult.style.backgroundColor = 'white';

  randomNumber = Math.floor(Math.random() * 100) + 1;
}
    
    function setGameOver() {
        guessField.disabled = true;
  guessSubmit.disabled = true;
  resetButton = document.createElement('button');
  resetButton.textContent = 'Start new game';
  document.body.appendChild(resetButton);
  resetButton.addEventListener('click', resetGame);
    }
    
 function checkGuess() {
 
      var userguess = Number(guessField.value);
      if(guessCount === 1)
      { guesses.textContent = 'Previous Guesses: '; }
           guesses.textContent += userguess + ' ';
           if(userguess === randomNumber)
           {lastResult.textContent = 'Congratulations! You got it right!';
            lastResult.style.backgroundColor = 'green';
           lowOrHi.textContent=' ';
            setGameOver();
       }
           else if(guessCount === 10)
               { lastResult.textContent = 'Game Over!';
                lastResult.style.backgroundColor = 'red';
                setGameOver();
               }
           else {
               lastResult.textContent = 'Wrong';
               if(userguess < randomNumber)
                   lowOrHi.textContent = 'Your Last guess was too low.';
               else
                   lowOrHi.textContent = 'Your Last guess was too high.';
               //guesses.textContent += userguess;
           }
       guessCount++;
           guessField.value = ' ';
           guessField.focus();
       }
    guessSubmit.addEventListener('click',checkGuess);
</script>
   
</body>
</html>
