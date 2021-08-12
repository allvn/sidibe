<template>
  <div id="app">
        <!-----------En fonction du type du component Select--------------->
    <Select :liste="pokemons" type="guide"></Select>
  </div>
</template>

<script>
import axios from "axios"; //Utilisation de Axios pour consommer des API
import Select from "./components/Select.vue";

export default {
  name: "App",
  components: {
    Select,
  },

  data() {
    return {
      pokemons:[]
    };
  },
/**La méthode GetList() nous renvoie 
 * 20 éléments depuis l'url
 */
  methods: {
    GetList() {
      axios.get("https://pokeapi.co/api/v2/pokemon/?offset=20&limit=20")//appel du point de terminaison de l’API Pokemon
      .then((data) => {
        this.pokemons = data.data.results;
      });
    }
  },
  mounted(){
    this.GetList();

  }
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
