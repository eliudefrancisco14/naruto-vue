<template>
  <div class="app">
    <SearchPerson />
  </div>
</template>

<script>

import SearchPerson from "@/components/SearchPerson.vue"

export default {
  name: "App",
  components:{ 
    SearchPerson
  }
  
};
</script>

<style>

#app {
  font-family: 'Ninja Naruto', sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 0;
  background-color: #ffe5a9;
}
</style>
