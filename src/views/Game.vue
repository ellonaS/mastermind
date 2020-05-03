<template>
  <div class="game">
    <b-form @submit="makeAGuess(guess)" v-for="guess in guesses" :key="guess.guessNumber">
      <b-row>
        <b-col sm="1">
          <span>{{guess.guessNumber}}</span>
        </b-col>
        <b-col v-for="color in gameComplexity" :key="color" sm="2">
          <game-board :class="guess.guessNumber" required></game-board>
        </b-col>
        <b-col sm="2">
          <b-button
            type="submit"
            squared
            variant="outline-secondary"
            :class="guess.guessNumber"
          >Submit Your Code</b-button>
        </b-col>
        <b-col sm="1">
          <span>Correct: {{guess.correct}}; misplaced: {{guess.misplaced}}</span>
        </b-col>
      </b-row>
    </b-form>
    <span>{{message}}</span>
    <b-row v-if="isGameOver">
      <b-col v-for="(color, index) in computerGeneratedColors" :key="index" sm="2">
        <div>{{color}}</div>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import GameBoard from "@/components/GameBoard.vue";

export default {
  name: "Game",
  data() {
    return {
      isGameOver: false,
      message: "",
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
  computed: {
    computerGeneratedColors() {
      return this.randomCode.map(x => {
        if (x === 1) {
          return "Red";
        } else if (x === 2) {
          return "Blue";
        } else if (x === 3) {
          return "Yellow";
        } else if (x === 4) {
          return "Green";
        } else if (x === 5) {
          return "Purple";
        } else if (x === 6) {
          return "Gray";
        }
      });
    }
  },
  created() {
    const min = 1;
    const max = 6;
    //Getting a random integer between two values
    //returns a random number between min and max (both included):
    for (let i = 1; i <= this.gameComplexity; i++) {
      this.randomCode.push(Math.floor(Math.random() * (max - min + 1) + min));
    }
    return this.randomCode;
  },
  methods: {
    disableButton(guess) {
      document
        .getElementsByClassName(guess.guessNumber)
        .forEach(element => (element.disabled = true));
    },
    makeAGuess(guess) {
      //disable button to prevent resubmission
      this.disableButton(guess);
      //select all input elements in the specified guess
      const colorsSelected = document.getElementsByClassName(guess.guessNumber);
      const guessedCode = [];
      //iterate through select divs, read their input values and save them in the array
      colorsSelected.forEach(element => {
        //parsing string value to int
        guessedCode.push(parseInt(element.value));
      });
      this.checkGuess(
        guessedCode.slice(0, guessedCode.length - 1),
        guess.guessNumber
      );
    },
    isGameWon(guessedCode, guessNumber) {
      guessedCode = guessedCode.filter(element => element === null);
      if (guessedCode.length === 0) {
        this.messsage = "you won!";
        this.isGameOver = true;
      } else if (guessNumber == "guess10") {
        this.message = "game over";
        this.isGameOver = true;
      } else this.message = "keep guessing";
    },
    checkGuess(guessedCode, guessNumber) {
      //create a clone of the real code to count misplaced colors
      let randomCodeClone = this.randomCode.map(x => x);
      this.guesses.forEach((item, index) => {
        if (item.guessNumber == guessNumber) {
          //finds the correct guessnumber to evaluate the guess and save it
          item.colors = guessedCode;
          //create a clone of the guessed code to count misplaced colors
          guessedCode = guessedCode.map(x => x);
          for (let i = 0; i < randomCodeClone.length; i++) {
            //compares the guess and the real code
            if (this.randomCode[i] === item.colors[i]) {
              //check for colors in the correct position
              this.guesses[index].correct += 1;
              //null values that have been guessed correctly
              randomCodeClone[i] = null;
              guessedCode[i] = null;
            }
          }
          //check if the color is misplaced
          for (let i = 0; i < randomCodeClone.length; i++) {
            for (let j = 0; j < randomCodeClone.length; j++) {
              if (guessedCode[i] === randomCodeClone[j] && guessedCode[i] != null) {
                this.guesses[index].misplaced += 1;
                randomCodeClone[j] = null;
                //break out of the loop if the match was found
                break;
              }
            }
          }
          this.isGameWon(guessedCode, guessNumber);
        }
      });
    }
  }
};
</script>

<style scoped>
</style>