<template>
  <div>
    <h1>Game Tebak Kata</h1>
    <p v-if="!gameOver">Tebak kata ini: {{ targetWord }}</p>
    <input v-model="guess" v-if="!gameOver" type="text">
    <button v-if="!gameOver" @click="checkGuess">Submit</button>
    <p v-if="gameOver">Hasil: {{ result }}</p>
    <button @click="restartGame" v-if="gameOver">Mulai lagi</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      words: ['apel', 'jeruk', 'mangga', 'pisang', 'anggur'],
      targetWord: '',
      guess: '',
      gameOver: false,
      result: ''
    };
  },
  methods: {
    checkGuess() {
      if (this.guess.toLowerCase() === this.targetWord) {
        this.result = 'Tebakan benar!';
      } else {
        this.result = 'Tebakan salah! Kata yang benar adalah ' + this.targetWord + '.';
      }
      this.gameOver = true;
    },
    restartGame() {
      this.targetWord = this.getRandomWord();
      this.guess = '';
      this.gameOver = false;
      this.result = '';
    },
    getRandomWord() {
      const randomIndex = Math.floor(Math.random() * this.words.length);
      return this.words[randomIndex];
    }
  },
  mounted() {
    this.targetWord = this.getRandomWord();
  }
};
</script>
