<template>
  <div class='counter' :class='{hidden: hiddenEl}'>
    <h2>Counter {{id}} score : <span class="score">{{counter}}</span></h2>
    <button @click='up'>Up</button>
    <button @click='down'>Down</button>
    <button @click='get'>Get</button>
    <label>Type new value:</label>
    <input type='number' v-model='settingValue' @keyup.enter='set'>
    <button @click='set'>Set</button>
    <button @click='resetCounter'>Reset</button>
    <button @click='removeCounter' class='remove'>Remove counter</button>
  </div>
</template>

<script>
  export default {
    name: 'Counter',
    props: ['countVal', 'formatVal', 'counterId', 'sel'],
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
        alert('Counter ' +this.id+ ' score is: ' + this.count)
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
  h2 {
    -webkit-margin-before:0;
    -webkit-margin-after:0;
    margin-bottom: 10px;
    letter-spacing: 1px
  }
  .counter {
    height: 100px;
    transition: height 1s
  }
  .hidden {
    visibility: hidden;
    height: 0px;
    z-index: -1
  }
  input {
    width: 80px
  }
  button.remove {
    background-color: #FF3030;
    color: #fff
  }
</style>