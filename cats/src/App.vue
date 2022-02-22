<template>
  <div id="App" class="bgcolors">
    <nav class="navbar navbar-light bg-light">
      <div class="container-fluid d-flex justify-content-center">
        <a class="navbar-brand" href="#">Random Gif Cat</a>
      </div>
    </nav>

    <div class="container">
      <div class="d-flex justify-content-center">
        <form @submit.prevent="getCat">
          <div class="row g-3 align-items-center my-3 mx-3">
            <div class="col-auto">
              <label class="col-form-label"> Titulo </label>
            </div>
            <div class="col-auto">
              <input type="text" class="form-control" v-model="titleCat" />
            </div>
          </div>
          <div class="row g-3 align-items-center my-2 mx-3">
            <div class="col-auto">
              <label class="col-form-label"> Filtro </label>
            </div>
            <div class="col-auto ">
              <select class="form-select" @change="filterCat($event)">
                <option value="">Selecciona una opción</option>
                <option
                  v-for="(filter, index) in filters"
                  :key="index"
                  :value="filter"
                  v-text="filter"
                ></option>
              </select>
            </div>
          </div>
          <div class="row g-3 align-items-center my-2 mx-3">
            <div class="col-auto">
              <label class="col-form-label"> Color </label>
            </div>
            <div class="col-auto">
              <select class="form-select" @change="catColor($event)">
                <option value="">Selecciona una opción</option>
                <option
                  v-for="(color, index) in colors"
                  :key="index"
                  :value="color.color"
                  v-text="color.text"
                ></option>
              </select>
            </div>

            <div class="col-auto">
              <div class="circle" :style="{backgroundColor: color}"></div>
            </div>
            <div class="col-auto">
              
            </div>
            
          </div>
          <div class="row g-3 align-items-center my-2">
            <div class="col-auto">
              <label class="col-form-label"> Tamaño </label>
            </div>
            <div class="col-auto">
              <input type="text" class="form-control" v-model="sizeCat" />
            </div>
            <button type="submit" class="btn btn-outline-success">
              Obtener Gatito
            </button>
          </div>
        </form>
      </div>
    </div>
    <div class="container mt-5">
      <div class="d-flex justify-content-center mb-2">
        <div>
          <img :src="image" />
        </div>
      </div>
     <HelloWorld />
    </div>
  </div>
 
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  data() {
    return {
      image: "",
      titleCat: "",
      sizeCat: "",
      filter: "",
      color: "",
      filters: ["blur", "mono", "sepia", "negative", "paint", "pixel"],
      colors: [
        { color: "green", text: "Verde" },
        { color: "blue", text: "Azul" },
        { color: "red", text: "Rojo" },
        { color: "white", text: "Blanco" },
        { color: "black", text: "Negro" },
      ],
    };
  },
  components: {
    HelloWorld,
  },

  methods: {
    getCat() {
      this.image = this.urlCat;
    },
    filterCat(event) {
      this.filter = event.target.value;
    },
    catColor(event) {
      this.color = event.target.value;
    },
  },
  computed: {
    urlCat() {
      return `https://cataas.com/cat/gif/says/${this.titleCat}?filter=${this.filter}&color=${this.color}&size=${this.catTamanio}`;
    },
  },
};
</script>

<style>
.circle {
  width: 15px;
  height: 15px;
  background-color: '';
  border-radius: 15px;
  border: .5px solid gray;
}
.bgcolors{
  background-color: rgb(215, 248, 237);
}

input {
  width: 220px !important;
}
select {
  width: 220px !important;
}


</style>
