<template>
<div>
  <div class="master">
        
        <img v-if="!item.includes('Text')" :src="require(`../assets/${item}Img/${item}${imgNumber % 24}.png`)" alt="test image" />

        <div v-else-if="item === 'Text1'">
          <pre>
Welcome to the DIY fan filter interactive tutorial. Follow the instructions in the top left and press continue to begin.
          </pre>
        </div>

        <div v-else>
          <pre>
Thank you for completing the interactive tutorial. For more information please visit our website or follow us on social media.
          </pre>
        </div>  
    
  </div>
</div>
</template>

<script>

export default {
  data: () => {
    return {
      imgNumber: 13, // 13 default because that is correct rotation direction
    }
  },
  props: [
    'item',
  ],
  methods: {
    moveImage(direction) {
      if (direction && this.imgNumber === 0) { 
          this.imgNumber = 24; 
      } else { direction ? this.imgNumber--:this.imgNumber++; }
    },
    check() {
      // error check
      return this.imgNumber % 24 === 13;
    },
  },
  watch: {
    item() {
      if (this.item === 'Tape' || this.item === 'CombinedFilter') {
        this.imgNumber = 13;
      } else {
        this.imgNumber = (Math.round(Math.random() * 24) + 1);
      }
    },
  },
}
</script>

<style scoped>
img {
  max-height: 70vh;
  width: auto;
  object-fit: cover;
}
div.master {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
pre {
  white-space: pre-wrap;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 2ch;
}
</style>

