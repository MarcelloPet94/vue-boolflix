<template>
  <div id="app">
    <Headercomp @passaDaHeader = "assegnaValoreDaHeader"/>
    <Main  
    :passaserie = tuttiSerieData
    :passafilm = tuttiFilmData
    />
  </div>
</template>

<script>
import axios from 'axios'
import Headercomp from './components/Headercomp.vue'
import Main from './components/Main.vue'

export default {
  name: 'App',
  components: {
    Headercomp,
    Main
  },

  data(){
    return{
      urlMovie: 'https://api.themoviedb.org/3/search/movie',
      urlTv: 'https://api.themoviedb.org/3/search/tv',
      serverImg: 'https://image.tmdb.org/t/p/',
      appValore: '',
      tuttiFilmData : [],
      tuttiSerieData: [],      
    }
  },

  methods: {
    assegnaValoreDaHeader( daHeader )
    {
      this.appValore = daHeader
      this.listaFilm()
      this.listaTv()
    },

    listaFilm(){
      axios.get(this.urlMovie , {
        params: {
          api_key : 'b1d73429cc8d9b6cc6dd4b3887ce83df',
          query : this.appValore
        }
      })
      .then((response) => {
        console.log('trova film')
        this.tuttiFilmData = response.data.results  
        console.log(this.tuttiFilmData[1]);
        
      })
      .catch(function (error) {
        console.log(error);
      });  
    },

    listaTv(){
      axios.get(this.urlTv , {
        params: {
          api_key : 'b1d73429cc8d9b6cc6dd4b3887ce83df',
          query : this.appValore
        }
      })
      .then((response) => {
        console.log('trova serie')
        this.tuttiSerieData= response.data.results  
        
      })
      .catch(function (error) {
        console.log(error);
      });  
    }     

  }
}
</script>

<style lang="scss">
@import './assets/style/global.scss';
</style>
