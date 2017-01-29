<template>
  <div class='counter' :class='{hidden: hiddenEl}'>
    <h1>Counter {{id}}: <span class="score">{{counter}}</span></h1>
      <button @click='up'>Up</button>
      <button @click='down'>Down</button>
      <button @click='get'>Get</button>
      <label>Type new value:</label>
      <input type='number' v-model='settingValue'>
      <button @click='set'>Set</button>
      <button @click='resetCounter'>Reset</button>
      <button @click='removeCounter'>Remove counter</button>
  </div>
</template>

<script>
  export default {
    name: 'Counter',

    props: ['countVal', 'formatVal', 'counterId'],

    data() {
      return { 
        count: this.countVal,
        format: this.formatVal,
        id: this.counterId,
        settingValue: 0,
        hiddenEl: false
      }
    },

    methods: {
      up() {
        if(this.count==Math.pow(10,this.format)-1) return false
        else this.count++
      },
      down() {
        if(this.count==0) return false
        else this.count--
      },
      get() {
        alert('Counter score is: ' + this.count)
      },
      set() {
        if (this.settingValue % 1 === 0 && this.settingValue >= 0 && this.settingValue<=Math.pow(10,this.format)-1) this.count = this.settingValue
        else alert ('Invalid value (must be integer between 0 and max format range)')
      },
      resetCounter() {
        this.count = 0
      },
      removeCounter() {
        this.hiddenEl = true
      }
    },

    computed: {
      counter() {
        let countLen = this.count.toString().length
        let countDiff = this.format - countLen
        let zeros = ''
        for (let i = 0; i < countDiff; i++) zeros += '0'
        return zeros+this.count
      }
    }
  }
</script>

<style scoped>
  h1 {
    -webkit-margin-before:0em;
    -webkit-margin-after:0em;
    margin-bottom: 10px
  }
  .counter {
    height: 100px;
  }
  .hidden {
    visibility: hidden;
    margin-top: -100px;
    z-index: -1
  }
</style>