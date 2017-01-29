<template>
  <div id="app">
    <h1>{{welcomeMsg}}</h1>
    <counter 
      v-for='counter in counters'
        :countVal='counter.count'
        :formatVal='counter.format'
        :counterId='counter.id'
    ></counter>
    <form>
      <label>Initial value:</label>
      <input type='number' v-model='initCount'>
      <label>Format:</label>
      <input type='number' v-model='initFormat' @keyup.enter='addNew'>
      <button type='button' id='addCounter' @click='addNew'>Add new counter</button>
    </form>
  </div>
</template>

<script>
  import Counter from './components/Counter.vue';
  export default {
    name: 'app',
    components: {
      Counter
    },
    data() {
      return{
        welcomeMsg: 'Welcome to score counters',
        initCount: '',
        initFormat: '',
        counters: [
          {
            count: 42,
            format: 3,
            id: 1
          },
          {
            count: 6,
            format: 2,
            id: 2
          },
          {
            count: 2,
            format: 1,
            id: 3
          },
          {
            count: 2384,
            format: 5,
            id: 4
          }
        ]
      }
    },
    methods: {
      addNew(){
        if (this.initFormat<this.initCount.toString().length) alert('Initial value is out of its format range')
        else if(this.initFormat<=0) alert('Initial format is too small (must be at least 1)')
        else if(this.initCount<0) alert('Initial value is below 0 (restricted)')
        else if(this.initCount % 1 !== 0) alert('Initial value is not an integer')
        else this.counters.push({
          count: this.initCount,
          format: this.initFormat,
          id: this.counters.length+1
        })
      }
    }
  }
  
</script>

<style>
  #app {
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    font-family: Arial, Helvetica, sans-serif
  }
  h1, h2 {
    letter-spacing: 5px;
    font-family: Impact, sans-serif
  }
  form input {
    width: 40px;
    margin-right: 10px
  }
  button {
    border: none;
    background-color: #d6d6d6;
    border-radius: 5px;
    padding: 5px 15px;
    font-weight: bold;
    margin: 0 5px 0 0;
    cursor: pointer
  }
  button#addCounter {
    background-color: #4CBB17;
    color: #fff
  }
  label {
    margin-left: 10px;
    font-family: Arial;
    font-weight: bold
  }
</style>
