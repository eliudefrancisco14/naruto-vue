<template>
  <div class="container">
    <div class="row">
      <div v-if="dataApi" class="col-md-6">
        <div v-for="data in dataApi.kekkeigenkai" :key="data.id">
          <ul>
            <li >{{ data.name }}</li>
            <img :src="data.characters[0].images[0]" :alt="data.name">
          </ul>
        </div>
      </div>
      <div v-else class="col-md-6">
        Loading...
      </div>
    </div>
    
  </div>
  
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data(){
    return {
      dataApi: null,
    }
  },
  async mounted() {
    try {
      const response = await axios.get("kekkei-genkai?page=1&limit=5");
      this.dataApi = response.data;
      console.log(response);
    } catch (error) {
      console.error("Erro na solicitação HTTP:", error);
    }
  },
};
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
