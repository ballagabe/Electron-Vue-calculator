<template>
  <div class="container">
    <div class="history">
      <div v-if="!proc">
        {{result}}
        {{opsymb}}
        {{displayNum}}  
      </div>    
    </div>
    <div class="row justify-content-end">
      <div class="col pt-4 pb-3">
        <div class="panel">{{ displayNum }}</div>
      </div>
    </div>

    <div class="row justify-content-center">
        <b-button v-on:click="ac" class="btn btn-primary btn-circle btn-sm">AC</b-button>
        <b-button v-on:click="plusminus" class="btn btn-primary btn-circle btn-sm">+/-</b-button>
        <b-button v-on:click="calc('%')" class="btn btn-primary btn-circle btn-sm">%</b-button>
        <b-button v-on:click="calc('/')" class="btn btn-warning btn-circle btn-sm">/</b-button>


        <b-button v-on:click="display(7)" class="btn btn-primary btn-circle btn-sm">7</b-button>
        <b-button v-on:click="display(8)" class="btn btn-primary btn-circle btn-sm">8</b-button>
        <b-button v-on:click="display(9)" class="btn btn-primary btn-circle btn-sm">9</b-button>
        <b-button v-on:click="calc('X')" class="btn btn-warning btn-circle btn-sm">X</b-button>

        <b-button v-on:click="display(4)" class="btn btn-primary btn-circle btn-sm">4</b-button>
        <b-button v-on:click="display(5)" class="btn btn-primary btn-circle btn-sm">5</b-button>
        <b-button v-on:click="display(6)" class="btn btn-primary btn-circle btn-sm">6</b-button>
        <b-button v-on:click="calc('-')" class="btn btn-warning btn-circle btn-sm">-</b-button>

        <b-button v-on:click="display(1)" class="btn btn-primary btn-circle btn-sm">1</b-button>
        <b-button v-on:click="display(2)" class="btn btn-primary btn-circle btn-sm">2</b-button>
        <b-button v-on:click="display(3)" class="btn btn-primary btn-circle btn-sm">3</b-button>
        <b-button v-on:click="calc('+')" class="btn btn-warning btn-circle btn-sm">+</b-button>

        <b-button v-on:click="display(0)" pill class="btn btn-primary btn-sm zero">0</b-button>
        <b-button v-on:click="dot" class="btn btn-primary btn-circle btn-sm">.</b-button>
        <b-button v-on:click="displayRes" class="btn btn-warning btn-circle btn-sm">=</b-button>
    </div>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Calculator',
  components: {
  },
  data: function () {
    return {
      displayNum: '',
      result: null,
      opsymb: '',
      proc: false
    }
  },
  methods: {
    display: function (num) {
      if(!this.proc) this.displayNum += '' + num
    },
    dot: function () {
      if(this.displayNum){
        !this.displayNum.includes('.') ? this.displayNum += '.' : null
      }
    },
    plusminus: function () {
      if(parseInt(this.displayNum) > 0){
        this.displayNum *= -1
      }else{
        this.displayNum *= -1
      }
    },
    ac: function () {
      this.displayNum = ''
      this.result = null,
      this.opsymb = '',
      this.proc = false
    },
    calc: function (type) {
      if(type == '+'){
        this.opsymb = '+'
        this.result = this.result + parseFloat(this.displayNum)
      }
      if(type == '-'){
        this.opsymb = '-'
        this.result = parseFloat(this.displayNum)
      }
      if(type == 'X'){
        this.opsymb = 'X'
        this.result = parseFloat(this.displayNum)
      }
      if(type == '/'){
        this.opsymb = '/'
        this.result = parseFloat(this.displayNum)
      }
      if(type == '%'){
        this.opsymb = '%'
        this.result = parseFloat(this.displayNum)
      }
      this.displayNum = ''
      this.proc = false
    },
    displayRes: function () {
      if(this.result){
        if(this.opsymb == '+') this.displayNum = (parseFloat(this.displayNum) + parseFloat(this.result)).toFixed(10)
        if(this.opsymb == '-') this.displayNum = (parseFloat(this.result) - parseFloat(this.displayNum)).toFixed(10)
        if(this.opsymb == 'X') this.displayNum = (parseFloat(this.result) * parseFloat(this.displayNum)).toFixed(10)
        if(this.opsymb == '/') this.displayNum = (parseFloat(this.result) / parseFloat(this.displayNum)).toFixed(10)
        if(this.opsymb == '%') this.displayNum = (parseFloat(this.result) % parseFloat(this.displayNum)).toFixed(10)
        this.result = 0
        this.opsymb = ''
        this.proc = true
      }
    }
  }
  
}
</script>

<style>
  .panel{
    font-size:2em;
    padding-left:16px;
    height:40px;
    max-width:180px
  }
  .btn{
    font-size:1.9em;
    margin: 0.4em 0.4em 0 0.4em
  }
  .btn-circle{ 
    width: 60px;
    height: 60px;
    padding: 10px 12px;
    border-radius: 35px;
    font-size: 1.1em;
    text-align: center
  }
  .zero{
    width:125px
  }
  .history{
    height:10px
  }
</style>
