<template>
<div>
  <!-- Rotate -->
  <div v-show="!itemArr[itemNum].includes('Text') && !itemArr[itemNum].includes('CombinedFilter') && !itemArr[itemNum].includes('Tape')" class="button-container">
    <button @click="$refs.tutorial.moveImage(false)">Left</button>
    <button @click="$refs.tutorial.moveImage(true)">Right</button>
  </div>
  <h1>{{ isError ? "ERROR":"" }}</h1>
  <h1 class="instructions">Instructions go here!</h1>
  <!-- Continue -->
  <button v-show="itemNum < itemArr.length-1" @click.left="check()">Continue</button>
  <center>
    <div >
      <TutorialView ref="tutorial" :item="itemArr[itemNum]" />
    </div>
  </center>
</div>
  
</template>

<script>

import TutorialView from './components/TutorialView.vue'

export default {
  name: 'App',
  data: () => {
    return {
      itemNum: 0,
      itemArr: ['Text1' , 'Fan', 'Filter', 'Tape', 'CombinedFilter', 'Text2'],
      isError: false,
    }
  },
  components: {
    TutorialView
  },
  methods: {
    check() {
      this.isError = !this.$refs.tutorial.check();
      if (!this.isError) {
        this.itemNum++
      }
    }
  }
}
</script>

<style>
button, img {
  user-select: none;
}
div.button-container {
  margin: 2.5%;
  display: flex;
  flex-direction: row;
  justify-content: center;
  padding: 1vw;
  background:rgba(159, 178, 197, 0.671);
  border-radius: 10px;
}
button {
  height: 5vh;
  width: 5vw;
  background-color: white;
  border: 2px solid black;
  font-weight: bold;
  font-size: 1rem;
  border-radius: 10px;
  margin: 10px;
}
button:hover {
  background-color: rgb(175, 191, 241);
  box-shadow: 1px 1px 2px;
}
</style>
