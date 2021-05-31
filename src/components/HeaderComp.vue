<template>
  <div class="main">
    <h1>BOOLFLIX</h1>
    <div class="search">
      <input type="text" placeholder="Busca el Film"
                v-model="search">
      <button @click="buscarPeliculas">Search Peliculas</button>
      <button @click="buscarSeries">Search Series</button>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      search : "",
    }
  },
  methods:{
    buscarPeliculas(){
     this.$emit("buscaPelis",this.search)
    },

    buscarSeries(){
     this.$emit("buscaSeries",this.search)
    }
  }
}
</script>

<style lang="scss">
  .main{
    width: 100%;
    height: 100px;
    padding: 50px;
    background-color: black;
    color: red;
    display: flex;
    align-items: center;
    justify-content: space-between;
    button{
      margin-left: 10px;
    }
  }
</style>