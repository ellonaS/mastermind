<template>
  <div class="home">
    <b-row v-for="guess in guesses" :key="guess.guessNumber">
      <b-col v-for="color in gameComplexity" :key="color" md="2">
        <game-board :class="guess.guessNumber"></game-board>
      </b-col>
      <b-col md="2">
        <b-button squared variant="outline-secondary" @click="makeAGuess(guess)">Submit Your Code</b-button>
      </b-col>
      <b-col md="2">
        <span>Correct: {{guess.correct}}; misplaced: {{guess.misplaced}}</span>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import GameBoard from "@/components/GameBoard.vue";

export default {
  name: "Home",
  data() {
    return {
      gameComplexity: 4,
      randomCode: [],
      guesses: [
        { guessNumber: "guess1", misplaced: 0, correct: 0, colors: [] },
        { guessNumber: "guess2", misplaced: 0, correct: 0, colors: [] },
        { guessNumber: "guess3", misplaced: 0, correct: 0, colors: [] },
        { guessNumber: "guess4", misplaced: 0, correct: 0, colors: [] },
        { guessNumber: "guess5", misplaced: 0, correct: 0, colors: [] },
        { guessNumber: "guess6", misplaced: 0, correct: 0, colors: [] },
        { guessNumber: "guess7", misplaced: 0, correct: 0, colors: [] },
        { guessNumber: "guess8", misplaced: 0, correct: 0, colors: [] },
        { guessNumber: "guess9", misplaced: 0, correct: 0, colors: [] },
        { guessNumber: "guess10", misplaced: 0, correct: 0, colors: [] }
      ]
    };
  },
  components: {
    GameBoard
  },
  created() {
    const min = 1;
    const max = 6;
    //Getting a random integer between two values
    //returns a random number between min and max (both included):
    for (let i = 1; i < 5; i++) {
      this.randomCode.push(Math.floor(Math.random() * (max - min + 1) + min));
    }
    return this.randomCode;
  },
  methods: {
    makeAGuess(guess) {
      //select all input elements in the specified guess
      const colorsSelected = document.getElementsByClassName(guess.guessNumber);
      const guessedCode = [];
      //iterate through select divs, read their input values and save them in the array
      colorsSelected.forEach(element => {
        guessedCode.push(parseInt(element.value));
      });
      this.checkGuess(guessedCode, guess.guessNumber);
    },
    checkGuess(guessedCode, guessNumber) {
      this.guesses.forEach((item, index) => {
        if (item.guessNumber == guessNumber) {
          //finds the correct guessnumber to evaluate the guess and save it
          item.colors = guessedCode;
          for (let i = 0; i < this.randomCode.length; i++) {
            //compares the guess and the real code
            if (this.randomCode[i] === item.colors[i]) {
              //check for colors in the correct position
              this.guesses[index].correct += 1;
              //parsing string value to int
            } else if (this.randomCode.indexOf(item.colors[i]) >= 0) {
              //check for misplaced colors
              console.log("counting misplaced");
              this.guesses[index].misplaced += 1;
            } else {
              console.log(this.randomCode.indexOf(item.colors[i]));
            }
          }
        }
      });
    }
  }
};
</script>
