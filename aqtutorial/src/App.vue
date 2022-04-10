<template>
<div>
  <!-- Instructions -->
  <h3 class="instructions">
    1. Use the left and right buttons to orient the fan away from you. The air should be moving into the screen.
  </h3>
  <h3 class="instructions">
    2. Use the left and right buttons to orient the filter the correct way. Look for arrow indicators on the side of the filter showing the direction of airflow.
  </h3>
  <h3 class="instructions">
    3. Seal the edges with duct tape to increase the efficiency of the filter and to hold the filter close against the fan.
     The less air that passes around the filter the better.
  </h3>
  <!-- Error Check -->
  <h1 class="error">{{ isError ? "Please orient the item as described in the instructions":"" }}</h1>

  <!-- Rotate -->
  <div v-show="!itemArr[itemNum].includes('Text') && !itemArr[itemNum].includes('CombinedFilter') && !itemArr[itemNum].includes('Tape')" class="button-container">
    <button @click="$refs.tutorial.moveImage(false)">Left</button>
    <button @click="$refs.tutorial.moveImage(true)">Right</button>
  </div>

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

import TutorialView from './components/TutorialView.vue';

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
    TutorialView,
  },
  methods: {
    check() {
      this.isError = !this.$refs.tutorial.check();
      if (!this.isError) {
        this.itemNum++;
      }
    },
  },
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

.error {
  color: red;
}
</style>
