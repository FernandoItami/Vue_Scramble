<template>
  <div class="main">
    <!--<div class="textdisplay">
      <label class="word" >{{text2}}</label>
      <label class="word">{{char}}</label>
    </div>-->
    <input type="text" v-model="input" @keypress.enter="textInput">
    <div class="textdisplay">
      <span class="lspace" v-for="(item, index) in letterarr" :key="index">
        <img class="bg" src="../assets/bg.png" alt="bg">
        <label class="word">{{item[indexlist[index].letter]}}</label>
      </span>
    </div>
    <button @click="textInput">scramble</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      scrambling: null,
      input: "",
      text: '',
      letterarr: [],
      indexlist: [],
      value: 28,
      char: '',
      list: ["_",".",",","A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"," ", "a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z"]
    }
  },
  mounted() {
    this.textInput()
    //var tidx = 0;
    //var lidx = 0;
    //var len = this.text.length;
    ////var dist = 0;
    //var speed = 50
    //var scramble = () => {
    //  if(tidx == len) {
    //    clearInterval(this),
    //    this.text2 = this.text2.slice(0, len -1)
    //  }
    //  else if(this.list[lidx] === this.text[tidx]) {
    //    this.text2 = this.text2 + this.char,
    //    //lidx = 0;
    //    tidx ++
    //  } else {
    //    if(this.list.indexOf(this.text[tidx]) > lidx) {
    //      lidx++;
    //      //dist = this.list.indexOf(this.text[tidx]) - lidx
    //    }else {
    //      lidx--;
    //      //dist = lidx - this.list.indexOf(this.text[tidx])
    //      }
    //    this.char = this.list[lidx]
    //  }
    //}
    //setInterval(scramble, speed);
    for(let i = 0; i < 10; i++) {
      this.letterarr.push(this.list)
    }
    for(let i = 0;i < 10; i++) {
      this.indexlist.push({letter:29})
    }
  },
  methods: {
    textInput() {
      this.text = this.input
      this.scramble()
      this.input = ''
    },
    scramble() {
      //var dist = Math.round((29 - this.text.length) / 2);
      this.letterarr = []
      for(let i = 0;i < this.text.length; i++) {
        this.letterarr.push(this.list)
        this.indexlist.push({letter:29})
      }
      for(let idx in this.indexlist) {
        this.scrambling = setInterval(() => {
          if (this.indexlist[idx].letter === this.list.indexOf(this.text[idx])) clearInterval(this.scrambling);
          else if (this.indexlist[idx].letter < this.list.indexOf(this.text[idx])) {
            this.indexlist[idx].letter++
          } else this.indexlist[idx].letter--
        }, 70)
      }
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
  min-height: 160px;
  min-width: 90%;
  margin: 20px 0 20px 0;
  background-color: grey;
}
</style>