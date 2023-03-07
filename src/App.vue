<template>
  <h1>Program 4: Website + Storage</h1>
  <Button text="Load Data" color="blue"></Button>
  <Button text="Clear Data" color="red"></Button>
  <QueryForm/>
  <Button text="Query" color="green"></Button>
</template>

<script>
import Button from  './components/Button.vue'
import QueryForm from './components/QueryForm.vue'

export default {
  name: 'App',
  components: {
    Button,
    QueryForm
  },
  data() {
    return {
      // to store query results from cosmos DB
      query_results: []
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

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

</style>
