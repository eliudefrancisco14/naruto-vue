<template>
  <div class="container">
    <div class="center">
      <div class="header">
        <div class="img">
          <img class="image-person" src="../assets/person.jpg" alt="Person" />
        </div>
        <div v-if="allData"  class="name">
          {{ allData.name }}
        </div>
        <div v-else>
          Nome do Personagem
        </div>
      </div>
      <div class="body">
        <form @submit.prevent="search">
          <div class="form-group">
            <input
              class="form-control"
              type="text"
              name="person"
              id="person"
              v-model="person"
            />
          </div>
          <div class="btn-group">
            <button class="btn">Pesquisar</button>
          </div>

        </form>
      </div>
      <div class="row">
        <div v-if="allData" class="col-md-6">
          <div>
            <ul>
              <li>{{ data.name }}</li>
              <img :src="data.images" :alt="data.name" />
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "SearchPerson",
  data() {
    return {
      dataApi: null,
      person: "",
      allData: "",
      loading: false,
    };
  },
  methods: {
    async search() {
      try {
        const response = await axios.get("character");
        this.dataApi = response.data;

        // Filtrando para encontrar o personagem desejado
        const filteredCharacter = this.dataApi.characters.find(
          (character) =>
            character.name.toLowerCase() === this.person.toLowerCase()
        );

        const nomes = this.dataApi.characters.map(n => n.name)
        const foundPerson = nomes.find(name => name === this.person);

        console.log(foundPerson);
        console.log(this.person)

        if (filteredCharacter) {
          this.allData = filteredCharacter;
        } else {
          console.log("Personagem não encontrado");
        }
      } catch (error) {
        console.error("Erro na solicitação HTTP:", error);
      }
    },
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
.body {
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
.btn:hover {
  background-color: #eeab0f;
  color: #fff;
}
.btn:active {
  background-color: #e0a10d;
  color: #fff;
}
.form-control {
  font-size: 18px;
  border: none;
  background-color: #fff2d4;
  border-radius: 10px;
  border-bottom: 2px solid #e0a10d;
  color: #e0730d;
  text-align: center;
}
</style>
