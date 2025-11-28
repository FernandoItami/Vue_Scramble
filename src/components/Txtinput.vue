<template>
  <div class="main">
    <div style="display:flex;justify-content:center;align-items:center">
      <input type="text" class="txtipt" v-model="input" @keypress.enter="textInput" placeholder="Type here...">
      <button @click="textInput" style="margin-left:20px">scramble</button>
    </div>
    <div class="textdisplay">
      <span class="lspace" v-for="(item, index) in letterarr" :key="index">
        <img class="bg" src="../assets/bg.png" alt="bg">
        <label class="word">{{item[indexlist[index].letter]}}</label>
      </span>
    </div>
    <label class="credits">Made with <a href="https://vuejs.org">Vue.js</a></label>
    <label class="credits">Font: Arcade by <a href="http://www.pizzadude.dk">Pizzadude</a></label>
  </div>
</template>

<script>
export default {
  // Fix: Explicitly name the component with multiple words
  name: 'TextInput', 
  data() {
    return {
      scrambling: null,
      input: 'Blackmule Scramble',
      text: '',
      letterarr: [],
      indexlist: [{letter:29}],
      char: '',
      list: ["_",".",",","A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"," "]
    }
  },
  mounted() {
    this.textInput()
  },
  methods: {
    async textInput() {
      this.text = this.input.toUpperCase()
      this.scramble()
      this.input = ''
    },
    scramble() {
      // Clear previous data
      this.letterarr = [] 
      
      // Reset indexlist to match new text length
      this.indexlist = [] 
      
      for(let i = 0; i < this.text.length; i++) {
        this.letterarr.push(this.list)
        this.indexlist.push({letter: 29, interval: null}) // Store interval per letter
      }

      // Loop through each letter position
      this.indexlist.forEach((item, idx) => {
        // Assign a unique interval for each letter
        item.interval = setInterval(() => {
          const targetIndex = this.list.indexOf(this.text[idx])
          
          if (item.letter === targetIndex) {
            clearInterval(item.interval)
          } else {
            // Randomize until match
            item.letter = Math.floor(Math.random() * this.list.length)
          }
        }, 30)
      })
    }
  },
}
</script>

<style>
.main {
  display: flex;
  flex-direction: column;
  width: 100%;
  min-height: 80%;
  justify-content: center;
  align-items: center;
}
.txtipt {
  width: 300px;
  height: 30px;
  font-size: 20px;
}
.lspace {
  position: relative;
  min-width: 80px;
  height: 100px;
  overflow: hidden;
  margin: 0 2px 0 0;
  background-color: rgb(192, 192, 192);
}
.bg {
  position: absolute;
  top: 5px;
  left: 5px;
  height: 90px;
  opacity: 0.5;
}
.word {
  position: absolute;
  font-size: 153px;
  font-family: "arcade";
  line-height: 90px;
  top: 17px;
  left: 5px;
}
.textdisplay {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  min-height: 102px;
  min-width: 90%;
  margin: 20px 0 20px 0;
  background-color: rgb(0, 0, 0);
  border: 2px solid black;
  overflow: hidden;
}
.credits {
  margin-top: 20px;
  font-size: 20px;;

}
</style>
