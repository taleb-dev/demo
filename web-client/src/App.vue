<template>
  <div id="app">
    <div>
      <form>
        <label>Enter your index:</label>
        <input v-model="index" type="text"/>
        <button type="button" @click="handleSubmit()">Submit</button>
      </form>
      <h3>Indexes I have seen:</h3>
      <span v-for="item in seenIndexes" :key="item.number">
        {{item.number}},
      </span>
      <h3>Calculated Values</h3>
    </div>
  </div>
</template>

<script>
const http = require('axios');

export default {
  name: 'App',
  components: {
  },
  data:function() {
    return {
      seenIndexes:[],
      values:{},
      index:""
    }
  },
  beforeMount() {
    this.fetchIndexes();
    this.fetchValues();
  },
  methods:{
    fetchValues: async function () {
      const values = await http.get('/api/values/current');
      this.values = values.data;
    },
    fetchIndexes: async function () {
      const seenIndexes = await http.get('/api/values/all');
      this.seenIndexes = seenIndexes.data;
    },
    handleSubmit: async function(){
      await http.post('/api/values',{
        index:this.index
      });
      this.index = '';
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
