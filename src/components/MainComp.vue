<template>
  <div class="container">
    <!-- busqueda desde la header -->
    <header-comp @buscaPelis="cercaFilm" @buscaSeries="cercaSerie"/>
    <ul>
      <li v-for="(resultado, index) in resultados" :key="index">
        <div class="flip-card">
          <div class="flip-card-inner">
            <div class="flip-card-front">
              <img :src="imgURL+resultado.poster_path" alt="imagen no disponible" style="width:100%;height:300px;">
            </div>
            <div class="flip-card-back">
              <div>{{resultado.title}} {{resultado.name}}</div>
                <div v-if="bandiere.includes(resultado.original_language)"> 
                  <img :src="require(`../assets/${resultado.original_language}.png`)" alt="">
                </div>
                <div v-else>idioma {{resultado.original_language}}</div>
                <div class="stars">
                  voto
                  <div class="empy">
                    <div class="inner">
                      <i class="far fa-star"></i>
                      <i class="far fa-star"></i>
                      <i class="far fa-star"></i>
                      <i class="far fa-star"></i>
                      <i class="far fa-star"></i>
                    </div>
                  </div>
                  <div class="solid" :style="`width:${6.7*resultado.vote_average}px`">
                    <div class="inner">
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                    </div>
                  </div>
                </div>  
                <div>{{resultado.overview}}</div>
            </div>
          </div>
        </div>
      </li>
    </ul>
    <!-- predeterminado -->
    <ul>
      <li v-for="(noresultado, index) in no_resultados" :key="index">
        <div class="flip-card">
          <div class="flip-card-inner">
            <div class="flip-card-front">
              <img :src="imgURL+noresultado.poster_path" alt="no disponible" style="width:100%;height:300px;">
            </div>
            <div class="flip-card-back">
              <div>{{noresultado.title}} {{noresultado.name}}</div>
                <div v-if="bandiere.includes(noresultado.original_language)"> 
                  <img :src="require(`../assets/${noresultado.original_language}.png`)" alt="">
                </div>
                <div v-else>idioma {{noresultado.original_language}}</div>
                <div class="stars">
                  voto
                  <div class="empy">
                    <div class="inner">
                      <i class="far fa-star"></i>
                      <i class="far fa-star"></i>
                      <i class="far fa-star"></i>
                      <i class="far fa-star"></i>
                      <i class="far fa-star"></i>
                    </div>
                  </div>
                  <div class="solid" :style="`width:${6.7*noresultado.vote_average}px`">
                    <div class="inner">
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                    </div>
                  </div>
                </div>  
                <div>{{noresultado.overview}}</div>
            </div>
          </div>
        </div>
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
        no_resultados:[],
        resultados:[],
        link : "https://api.themoviedb.org/3/search/",
        api_key : "e88b7b00a17113604dd035c629927671",
        query : "",
        bandiere : [
          "en",
          "ja",
          "it"
        ],
        imgURL : 'https://image.tmdb.org/t/p/w342'
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
     axios.get("https://api.themoviedb.org/3/search/movie?api_key=e88b7b00a17113604dd035c629927671&query=batman&language=it-IT")
     .then(ress => {
       this.no_resultados = ress.data.results;
       console.log(ress.data.results)
     })
     .catch(err => {
       console.log(err)
     })
    }

  }
</script>

<style lang="scss">
  .flip-card {
  background-color: transparent;
  width: 100%;
  height: 100%;
  perspective: 1000px;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.6s;
  transform-style: preserve-3d;
  box-shadow: 2px 1px 10px 5px red;
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front, .flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}

.flip-card-front {
  background-color: #bbb;
  color: black;
}

.flip-card-back {
  padding: 5px;
  overflow: auto;
  background-color: black;
  color: white;
  transform: rotateY(180deg);
}
  .container{
    width: 100%;
    height: 100vh;
    background-image: url(https://wallpaperaccess.com/full/229832.jpg);
    background-size: cover;
    overflow: auto;
    ul{
      display: flex;
      flex-wrap: wrap;
      list-style: none;
      align-items: center;
      padding: 0px 70px;
      li{
        width: calc(100% / 6);
        min-width: 200px;
        height:300px;
        margin: 20px;
        font-size:12px;

        img{
          width: 25px;
        }
        
      }
    }
  }
  .stars{
    position: relative;
    .empy,.solid{
     position: absolute;
     top: 1px;
     left: 30px;
     overflow: hidden;
    }
    .inner{
      width: 150px;
    }
    .solid{
      color: gold;
    }
  }

</style>