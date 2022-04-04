<template>
  <div class="app">
    <!-- <h1>Pokemon</h1> -->

    <div class="centre">
      <img class="logo" height=100 id="id2" src="../assets/Pokemon Api.png" />
      <!-- <button v-on:click="clicked">click</button>
      <button v-on:click="hide">hide</button>
      <button v-on:click="show">show</button> -->


   <h2> Trouve ton Pokemon </h2>

      
      <div id="create"></div>

      <input
        autocomplete="off"
        type="number"
        id="name"
        name="name"
        min="0"
        max="898"
        required
        class="search"
        size="10"
        v-on:change="create"
      />

      <button class="btn" v-on:click="create">Rechercher</button>


      <div class="box">
        <div v-if="this.info" class="card">
          <div class="name">{{ this.nom }}</div>
          <div class="pv"><span class="pvLabel">pv</span> 117</div>
          <img class="pokemonImage"  :src="`${this.url}`" />
          <!-- <ul >
            <li v-for="move in this.move" :key="move.name">
              {{ move.name }}
            </li>
          </ul> -->
          <!-- <div class="line">
            <div class="title" >Poids:</div>
            <div>{{ this.poids }}</div>
          </div> -->
          <!-- <div class="line">
            <div >Poids</div>
            <div>{{ this.poids }}</div>
          </div> -->
          <!-- <div>{{ this.poids }}</div> -->
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "PokemonAPI",
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      info: null,
      nom: null,
      poids: null,
      url: null,
    };
  },
  methods: {
    clicked: function () {
      console.log("click");
    },
    hide: function () {
      console.log("hide");
      document.getElementById("idh1").style.display = "none";
    },
    show: function () {
      console.log("show");
      document.getElementById("idh1").style.display = "block";
    },
    create: function () {
      axios
        .get(
          "https://pokeapi.co/api/v2/pokemon/" +
            document.getElementById("name").value
        )
        .then((response) => {
          
          this.info = response.data;
  //         const just2move = this.info.moves.slice(2)
  // console.log(just2move)
          this.nom = this.info.name;
          this.poids = this.info.height;
          // this.move = just2move
          this.url = this.info.sprites.front_default;
        });
    },
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* app {
  background-color: #2832e0;
  } */

.logo {
  margin-bottom: 50px;
}

#src {
}

.search {
  box-sizing: border-box;
  width: 180px;
  height: 28px;
  outline: none;
  border: none;
  border: 1px solid #ccc;
  padding-left: 10px;
  border-radius: 3px;
}


.btn {
  cursor: pointer;
  outline: none;
  border: none;
  box-shadow: none;
  /* height: 28px; */
  border-radius: 3px;
  padding: 8px;
  margin-left: 10px;
  /* border: 1px solid #ccc; */

  transform: scale(1);
  background-color: rgb(62,84,164);
  color: rgb(242,192,10);
  font-weight: bold;

}

.line {
  display: flex;
  column-gap: 8px;
  margin-bottom: 3px;
}

.btn:active {
  transform: scale(0.97)
}

.box {
  display: flex;
  justify-content: center;
}

.pokemonImage {
  margin-top: 8px;
  width: 200px;
  border: 1px solid #eee;
  border-radius: 3px;
    margin-bottom: 3px;
  background-color: #fff;

}

.title {
  font-weight: bold;
}

.name {
  position: absolute;
  top: 2px;
  left: 5px;
    font-weight: bold;
  text-transform: capitalize;
}

.pv {
  position: absolute;
  top: 2px;
  right: 3px;
  font-weight: bold;
}

.pvLabel {
  font-weight: bold;
  font-size: 8px;
}

.card {
  position: relative;
  margin-top: 20px;
  width: 200px;
  padding: 20px;
  border: 8px solid rgb(242,192,10);  
  /* background-color: rgb(62,84,164); */


  border-radius: 6px
  /* border: 10px solid yellow; */
  /* border-radius: 6px; */
  /* background-color: #2832e0; */
}

</style>
