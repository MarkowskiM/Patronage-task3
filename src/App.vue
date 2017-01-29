<template>
  <div id="app">
    <h1>{{welcomeMsg}}</h1>
    <counter 
      v-for='counter in counters'
      :countVal='counter.count'
      :formatVal='counter.format'
      :counterId='counter.idx'
    ></counter>
    <form>
      <label>Initial value:</label>
      <input type='number' v-model='initCount'>
      <label>Format:</label>
      <input type='number' v-model='initFormat' placeholder='>0'>
      <button type='button' id='addCounter' @click='addNew'>Add new counter</button>
      <!-- <button type='button' id='removeSelected'>Remove selected counters</button> -->
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
            idx: 1
          },
          {
            count: 6,
            format: 2,
            idx: 2
          },
          {
            count: 2,
            format: 1,
            idx: 3
          },
          {
            count: 84,
            format: 5,
            idx: 4
          }
        ]
      }
    },

    methods: {
      addNew(){
        if (this.initFormat<this.initCount.toString().length) alert('Initial value is out of its format range')
        else if(this.initFormat<=0) alert('Initial format is too small (must be at least 1)')
        else if(this.initCount<0) alert('Initial value is below 0 (restricted)')
        else this.counters.push({
          count: this.initCount,
          format: this.initFormat,
          idx: this.counters.length+1
        })
      }
    },

    computed: {

    }
  }
  
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
