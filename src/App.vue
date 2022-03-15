<template>
 <h1>Reaction Timer</h1>
 <button
     v-if="!isPlaying"
     class="btn primary"
     @click="start"
     :disabled="isPlaying">Play</button>
  <block-component
      v-if="isPlaying"
      :delay="delay"
      @end="endGame"
  ></block-component>
  <ResultsComponent
      v-if="showScore"
      :score="score"
  ></ResultsComponent>
</template>

<script>
import BlockComponent from "@/components/BlockComponent";
import ResultsComponent from "@/components/ResultsComponent";

export default {
  name: 'App',
  components: {
    ResultsComponent,
   BlockComponent,
  },
  data(){
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showScore: false
    }
  },
  methods: {
    start(){
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
      this.showScore = false
    },
    endGame(reactionTime){
      this.score = reactionTime
      this.isPlaying = false
      this.showScore = true
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}
body {
  font-family: Inter, Roboto, Oxygen, Fira Sans, Helvetica Neue, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 16px;
  color: #2c3e50;
  background: #2c3e50;
}
.btn {
  color: #42b983;
  position: relative;
  place-content: center;
  place-items: center;
  width: fit-content;
  border-radius: 99px;
  letter-spacing: 0.05em;
  border: 1px solid #42b983;
  text-decoration: none;
  text-transform: uppercase;
  margin-right: 10px;
  padding: 0.5rem 1.5rem;
  white-space: nowrap;
  font-weight: 700;

  background: #fff;
  transition: all 0.22s;
}

.btn:hover {
  cursor: pointer;
  opacity: 0.8;
}

.btn:active {
  box-shadow: inset 1px 1px 1px rgba(0, 0, 0, 0.3);
}
.btn.primary {
  background: #42b983;
  color: #fff;
}

.btn.danger {
  background: #e53935;
  color: #fff;
  border-color: #e53935;
}
</style>
