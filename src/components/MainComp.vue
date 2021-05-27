<template>
  <div class="container">
    <header-comp @buscaPelis="cercaFilm" @buscaSeries="cercaSerie"/>
    <ul>
      <li v-for="(resultado, index) in resultados" :key="index">
        <img src="" alt="">
        <div>{{resultado.title}} {{resultado.name}}</div>
        <div>{{resultado.original_language}}</div>
        <div>voto {{resultado.vote_average}}</div>
      </li>
    </ul>
  </div>
</template>

<script>
  import HeaderComp from './HeaderComp.vue'
  import axios from "axios"
  export default {
    components:{
      HeaderComp
    },
    data(){
      return{
        resultados:[],
        link : "https://api.themoviedb.org/3/search/",
        api_key : "e88b7b00a17113604dd035c629927671",
        query : ""
      }
    },

    methods:{
      cercaFilm(search){
        this.query = search;
        console.log(this.query);
        this.getLink("movie")
      },

       cercaSerie(search){
        this.query = search;
        console.log(this.query);
        this.getLink("tv")
      },

     

      getLink(type){
        axios.get(this.link+type,{
          params :{
            api_key : this.api_key,
            query : this.query,
            language :"it-IT"
          }
        })
        .then(res => {
          this.resultados = res.data.results
          console.log(this.resultados)
        })
        .catch(err => {
          console.log(err);
        })
      },
    },

    created(){
     
    }

  }
</script>

<style lang="scss">
  .container{
    width: 100%;
    height: 100vh;
    background-color: grey;
    overflow: auto;
    ul{
      display: flex;
      flex-wrap: wrap;
      list-style: none;
      align-items: center;
      padding: 0px 70px;
      li{
        width: calc(100% / 6);
        height: 180px;
        margin: 20px;
        border: solid black;
        text-align: center;
      }
    }
  }
</style>