<script setup>
import { ref, resolveTransitionHooks } from 'vue'
import { reactive } from 'vue'

defineProps({
  msg: String,
})

</script>

<template>
  <div>

    <h1>Rock Paper Scissors</h1>
    
    <div class="result">
      <img :src="leftChoice" v-if="leftChoice" />
      <img :src="rightChoice" v-if="rightChoice" />
      <p>{{ result }}</p>
    </div>
    <div class="score">
      <p>Score: {{ leftScore }} - {{ rightScore }}</p>
    </div>
    <button @click="playRound">Play</button>
    <button @click="resetScore">Reset</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      choices: ['rock', 'paper', 'scissors', 'love'],
      leftChoice: null,
      rightChoice: null,
      leftScore: 0,
      rightScore: 0,
      result: '',
    };
  },
  methods: {
    resetScore() {
      this.leftScore = 0;
      this.rightScore = 0;
    },
    playRound() {
      const leftIndex = Math.floor(Math.random() * this.choices.length);
      const rightIndex = Math.floor(Math.random() * this.choices.length);


      this.leftChoice = `${this.choices[leftIndex]}.jpg`;
      this.rightChoice = `${this.choices[rightIndex]}.jpg`;

      console.log(leftIndex)
      if (leftIndex === rightIndex) {
        this.result = "It's a tie!";
      } else if (
        (leftIndex === 0 && rightIndex === 2) ||
        (leftIndex === 1 && rightIndex === 0) ||
        (leftIndex === 2 && rightIndex === 1) ||
        (leftIndex === 3 && rightIndex === 0) ||
        (leftIndex === 3 && rightIndex === 1) ||
        (leftIndex === 3 && rightIndex === 2) 
      ) {
        this.result = 'left win!';
        this.leftScore++;
      } 
      else {
        this.result = 'right wins!';
        this.rightScore++;
      }
    },
  },
};
  
</script>

<style>
img {

  height: 300px;
  margin: 10px;

}
</style>

