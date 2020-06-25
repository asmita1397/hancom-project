<template>
  <div id="app">
    <Tab @testMethod="testMethod" :selected="selected"/>
    
  </div>
</template>

<script>

import Tab from "./components/Tab"

export default {
  name: "App",
  components: {
      Tab
  },
  data() {
    return {
      selected:""
    }
  },
  methods: {
      testMethod(data)
      {
        console.log("zzzzzzzzzzzzzzzzzz",data)
         this.selected=data
        console.log("ggggggg",this.selected)
      }
  },
  
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
 
}
</style>
