<template>
  <h1 class="display-5 mb-5">Pokedex</h1>

  <section class="container">
    <div class="d-flex align-content-around flex-wrap">
      <div class="p-2" v-for="(data, index) in pokemons" :key="index">
        <div class="card" style="width: 18rem">
          <div class="card-header">
            <h5>
              {{ index + 1 }}-<em class="shiny">Shiny</em> {{ data.name }}
            </h5>
          </div>
          <div class="card-body p-2">
            <img :src="data.img" />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      pokemons: [],
    };
  },
  created() {
    let instance = this;
    for (let i = 0; i < 898; i++) {
      axios
        .get(`https://pokeapi.co/api/v2/pokemon/${i + 1}`)
        .then((response) => {
          let pokemon = {
            name: response.data.name,
            img: response.data.sprites.front_shiny,
          };
          instance.pokemons.push(pokemon);
        })
        .catch((err) => {
          console.log(err);
        });
    }
    console.log(this.pokemons);
  },
};
</script>

<style>
.shiny {
  color: rgb(112, 112, 65);
}
img {
  padding: 20px;
}
.card:hover {
  box-shadow: 20px 20px 60px #bebebe, -20px -20px 60px #ffffff;
}
</style>