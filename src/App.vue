<template>
<div id="app">
 <div class="clac">
    <input class="ans" id="answer" disabled="disabled" :value="currentVal">
    <div class="keys">
      <div class="numkeys">
        <input class="button" type="button" v-on:click="enternum('1')" value="1">
        <input class="button" type="button" v-on:click="enternum('2')" value="2">
        <input class="button" type="button" v-on:click="enternum('3')" value="3">
        <input class="button" type="button" v-on:click="enternum('4')" value="4">
        <input class="button" type="button" v-on:click="enternum('5')" value="5">
        <input class="button" type="button" v-on:click="enternum('6')" value="6">
        <input class="button" type="button" v-on:click="enternum('7')" value="7">
        <input class="button" type="button" v-on:click="enternum('8')" value="8">
        <input class="button" type="button" v-on:click="enternum('9')" value="9">
        <input class="button" type="button" v-on:click="dot('.')" value=".">
        <input class="button" type="button" v-on:click="enternum('0')" value="0">
        <input class="button" type="button" v-on:click="calc()" value="=">
      </div>
      <div class="motkeys">
        <input class="button" type="button" v-on:click="plus()" value="+">
        <input class="button" type="button" v-on:click="minus()" value="-">
        <input class="button" type="button" v-on:click="multiply()" value="*">
        <input class="button" type="button" v-on:click="divided()" value="/">
        <input class="button" type="button" v-on:click="clear('C')" value="C">
      </div>
    </div>
  </div>
</div>
</template>

<script>


export default {
  name: "app",
  data(){
    return {
      currentVal: '',
    preNum: '',
    nextNum: '',
    toPlu: '',
    operator: '',
    keyInNextNum: false,
    ifdot: false,
    end: false,
    }
  },
  methods: {
     enternum: function(number){
      // console.log(this.currentVal)
      this.currentVal = this.currentVal.concat(number)
      if (this.keyInNextNum) {
        this.nextNum = this.currentVal
      }else if (this.end) {
        this.clear()
        this.currentVal = number
        this.end = false
      }else {
        this.preNum = this.currentVal
      }
    },
    dot: function(event){
      if (this.currentVal==""){
        this.currentVal = "0"
      }
      if (this.ifdot == false){
        this.currentVal = this.currentVal.concat(event)
        this.ifdot = true
        console.log(1)
      }
    },
    clear: function(){
      this.keyInNextNum = false
      this.operator = ""
      this.currentVal = ""
      this.ifdot = false
      this.end = false
    },
    plus: function(){
        this.ifdot = false
        if (this.operator !== ''){
          this.calc()
          this.preNum = this.currentVal
          this.operator = ''
          this.plus()
        }else{
          this.keyInNextNum = true
          this.preNum = this.currentVal
          this.currentVal = ''
          this.operator = '+'
        }     
    },
    minus: function(){
      this.ifdot = false
      if (this.operator !== ''){
          this.calc()
          this.preNum = this.currentVal
          this.operator = ''
          this.minus()
        }else{
          this.keyInNextNum = true
          this.preNum = this.currentVal
          this.currentVal = ''
          this.operator = '-'
        }
    },
    multiply: function(){
      this.ifdot = false
      if (this.operator !== ''){
          this.calc()
          this.preNum = this.currentVal
          this.operator = ''
          this.multiply()
      }else{
        this.keyInNextNum = true
        this.preNum = this.currentVal
        this.currentVal = ''
        this.operator = '*'
      }
    },
    divided: function(){
      this.ifdot = false
      if (this.operator !== ''){
          this.calc()
          this.preNum = this.currentVal
          this.operator = ''
          this.divided()
      }else{
        this.keyInNextNum = true
        this.preNum = this.currentVal
        this.currentVal = ''
        this.operator = '/'
      }
    },
    calc() {
      this.ifdot = false
      this.keyInNextNum = false
      this.end = true
      if (this.operator == '+') {
        // console.log(this.preNum)
        // console.log(this.nextNum)
        this.currentVal = String(parseFloat(this.preNum) + parseFloat(this.nextNum) )
      } else if (this.operator == '-') {
        this.currentVal = String(parseFloat(this.preNum) - parseFloat(this.nextNum) )
      } else if (this.operator == '*') {
        this.currentVal = String(parseFloat(this.preNum) * parseFloat(this.nextNum)) 
      } else if (this.operator == '/') {
        this.currentVal = String(parseFloat(this.preNum) / parseFloat(this.nextNum)) 
      } 
    }
  },
}
</script>

<style>
.numkeys {
  position: relative;
  display: flex;
  width: 250px;
  margin: 0px;
  flex-direction: row;
  flex-wrap: wrap;
}

.clac {
  position: absolute;
  border: solid 1px;
  width: 308px;
  left: 50%;
  top: 50%;
  transform: translate(-50%,-50%);
  
}

.button {
  position: relative;
  width: 50px;
  height: 50px;
  margin: 10px;
  border-radius: 100%;
  
  font-size: 25px;
}

.motkeys {
  display: flex;
  flex-direction: column;
  margin-left: -15px;
}

.keys {
  display: flex;
  margin-bottom: 15px;
}
.ans {
  width:300px;
  height:50px;  
  font-size: 30px;
  text-align: right;
}



</style>
