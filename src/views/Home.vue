<template>
  <div class="home">
    <h3>OBJECT OF THE GAME</h3>
    <p>
      The object of MASTERMIND is to guess computer-generated secret code consisting of a series of 4
      colors. Each guess results in feedback narrowing down the possibilities of the
      code. The player wins the game if the secret code is guessed within 10 or less guesses.
    </p>
    <h3>RULES</h3>
    <ol>
      <li>When you click "play" computer will generate a secret code of a series of 4 colors.</li>
      <li>Each row represents one guess. Make a guess by selecting colors from the dropdown option</li>
      <li>Duplicate colors are alllowed, but blank spaces are not permitted.</li>
      <li>To submit a guess click "SUBMIT YOUR CODE" button</li>
      <li>
        Computer will generate the feedback for you by providing the number of the right colors in the right positions
        (without indication of which color it corresponds to) and the number of the right colors in the wrong positions.
      </li>
      <li>You win the game if you guess the code within 10 or less guesses.</li>
      
    </ol>
  </div>
</template>

<script>
export default {
  name: "Home"
};
</script>

<style scoped>
</style>
