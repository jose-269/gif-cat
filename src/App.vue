<template>
  <div id="app">
    <header class="pt-5">
      <h1 class="m-0 pt-5 pb-4">Random Gif Cat</h1>
    </header>
    <main class="py-4">
      <div class="container">
        <div class="row">
          <div class="col-6 my-2 text-end">
            <h5 class="m-0">Título:</h5>
          </div>
          <div class="col-6 my-2 ps-0 text-start">
            <input
              type="text"
              placeholder="Ingresa un Título"
              v-model="titulo"
            />
          </div>
          <div class="col-6 my-2 text-end">
            <h5 class="">Filtro:</h5>
          </div>
          <div class="col-6 my-2 ps-0 text-start">
            <select v-model="filtro">
              <option disabled>Seleccione un filtro</option>
              <option v-for="el in filtros" :key="el">
                {{ el }}
              </option>
            </select>
          </div>
          <div class="col-6 my-2 text-end">
            <h5 class="">Color:</h5>
          </div>
          <div class="col-6 my-2 ps-0 text-start">
            <select v-model="color">
              <option disabled>Seleccione un color</option>
              <option
                v-for="el in colorSelect"
                :key="el.colorValor"
                :value="el.colorValor"
              >
                {{ el.colorNombre }}
              </option>
            </select>
          </div>
          <div class="col-6 my-2 text-end">
            <h5 class="">Tamaño:</h5>
          </div>
          <div class="col-6 my-2 ps-0 text-start">
            <input
              type="text"
              placeholder="Ingresa un tamaño"
              v-model="tamaño"
            />
          </div>
        </div>
      </div>
    </main>
    <section class="py-5">
      <div class="container">
        <div class="row">
          <div class="col-12 pb-4">
            <button
              @click="getData"
              type="button"
              class="btn rounded border-warning border-2"
            >
              Obtener mi gatito
            </button>
          </div>
          <div class="col-12">
            <img :src="gato && gato.config && gato.config.url" alt="" />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      gato: "",
      titulo: "",
      tamaño: "",
      filtros: ["blur", "mono", "sepia", "negative", "paint", "pixel"],
      filtro: "",
      colorSelect: [
        {
          colorNombre: "rojo",
          colorValor: "red",
        },
        {
          colorNombre: "azul",
          colorValor: "blue",
        },
        {
          colorNombre: "verde",
          colorValor: "green",
        },
        {
          colorNombre: "blanco",
          colorValor: "white",
        },
        {
          colorNombre: "amarillo",
          colorValor: "yellow"
        }
      ],
      color: "",
    };
  },
  methods: {
    async getData() {
      const url = `https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.tamaño}`;
      try {
        const req = await axios(url);
        this.gato = req;
        console.log(this.gato);
      } catch (error) {
        console.log(error);
      }
    },
    // filters() {
    //   console.log(this);
    // },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #090b06;
}
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
header {
  background-color: #86c600;
  h1 {
    font-size: 5rem;
  }
}
main {
  background-color: #c2f167;
}
section {
  background-color: #f52314;
  .btn {
    background-color: #86c600;
  }
}
.red {
  color: red;
}
.blue {
  color: blue;
}
.green {
  color: green;
}
.white {
  color: white;
}
.yellow {
  color: yellow;
}
</style>
