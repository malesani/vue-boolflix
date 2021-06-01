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
  input{
    height: 30px;
    width: 300px;
    padding-left: 10px;
    border-radius: 10px;
    outline: none;
    border: none;
  }
  button{
    padding: 8px;
    border-radius: 13px;
    cursor: pointer;
    color: red;
    background: black;
    border: black 1px solid;
    margin-left: 10px;
    
  }
  button:hover{
    border: white 1px solid;
  }
</style>