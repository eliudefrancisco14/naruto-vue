<template>
  <div class="container">
    <div class="center">
        <div class="header">
          <div class="img">
            <img class="image-person" src="../assets/person.jpg" alt="Person">
          </div>
            Nome do Personagem
        </div>
        <div class="body">
          <div class="form-group">
            <input class="form-control" type="text" name="person" id="person">
          </div>
          <div class="btn-group">
            <button class="btn">Pesquisar</button>
          </div>
        </div>
      <div class="row">
        <!-- <div v-if="dataApi" class="col-md-6">
          <div v-for="(data, i) in dataApi.kekkeigenkai" :key="i">
            <ul>
              <li>{{ data.name }}</li>
              <img :src="data.characters[0].images[0]" :alt="data.name" />
            </ul>
          </div>
        </div>
        <div v-else class="col-md-6">Loading...</div> -->
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "SearchPerson",
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

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  
}
.center {
  width: 400px;
  margin-left: auto;
  margin-right: auto;
  background-color: #eee;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0px 0px 3px #444;
  position: absolute;
}
img {
  height: 80px;
  border-radius: 40px;
  box-shadow: 0px 0px 4px #444;
  
}
.body{
  margin: 25px 0px;
  padding: 10px 0px;
}
.btn {
  margin: 10px 0px;
  font-size: large;
  border: none;
  background-color: #ffc53e;
  border-radius: 10px;
  padding: 10px;
  cursor: pointer;
}
.btn:hover{
  background-color: #eeab0f;
  color: #fff;
}
.btn:active {
  background-color: #e0a10d;
  color: #fff;
}
.form-control{
  font-size: 18px;
  border: none;
  background-color: #fff2d4;
  border-radius: 10px;
  border-bottom: 2px solid #e0a10d;
  color: #e0730d;
  text-align: center;
}

</style>
