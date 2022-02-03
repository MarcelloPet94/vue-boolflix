<template>
  <div>
      <SearchComp
      @ricercaFilm = "riassegnaDatoRicerca"
      />

      <div class="ricerca_container">
        <div class="box" v-for="film in tuttiFilmData" :key="film.id">
          <ul>
            <li>Titolo: {{film.title}}</li>
            <li>Titolo originale: {{film.original_title}}</li>

            <li v-if="film.original_language.toLowerCase() == 'it'"><img src='../assets/img/italy.png'></li>
            <li v-else-if="film.original_language.toLowerCase() == 'fr'"><img src='../assets/img/france.png'></li>
            <li v-else-if="film.original_language.toLowerCase() == 'de'"><img src='../assets/img/germany.png'></li>
            <li v-else-if="film.original_language.toLowerCase() == 'en'"><img src='../assets/img/united-kingdom.png'></li>

            <li v-else>{{film.original_language}}</li>
            <li>Voto: {{film.vote_count}}</li>
          </ul>
        </div>

        <div class="box serie" v-for="serie in tuttiSerieData" :key="serie.id">
          <ul>
            <li>Titolo: {{serie.name}}</li>
            <li>Titolo originale: {{serie.original_name}}</li>

            <li v-if="serie.original_language.toLowerCase() == 'it'"><img src='../assets/img/italy.png'></li>
            <li v-else-if="serie.original_language.toLowerCase() == 'fr'"><img src='../assets/img/france.png'></li>
            <li v-else-if="serie.original_language.toLowerCase() == 'de'"><img src='../assets/img/germany.png'></li>
            <li v-else-if="serie.original_language.toLowerCase() == 'en'"><img src='../assets/img/united-kingdom.png'></li>

            <li v-else>{{serie.original_language}}</li>
            <li>Voto: {{serie.vote_count}}</li>
          </ul>
        </div>        

      </div>
      
   </div>
</template>

<script>
import axios from 'axios'
import SearchComp from './partials/SearchComp.vue'

export default {
  name: 'Research',
  components: {
    SearchComp
  },

  data(){
    return{
      urlMovie: 'https://api.themoviedb.org/3/search/movie',
      urlTv: 'https://api.themoviedb.org/3/search/tv',
      titolo: '',
      tuttiFilmData : [],
      tuttiSerieData: []
    }
  },

  methods:{
    riassegnaDatoRicerca(inputRicerca){
      this.titolo = inputRicerca  
      this.listaFilm()
      this.listaTv()
    },


    listaFilm(){
      axios.get(this.urlMovie , {
        params: {
          api_key : 'b1d73429cc8d9b6cc6dd4b3887ce83df',
          query : this.titolo
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
          query : this.titolo
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

<style scoped lang="scss">
  .ricerca_container 
  {
    display: flex;
    flex-wrap: wrap;

    .box
    {
      width: 30%;
      min-height: 200px;
      padding: 16px;
      background-color: rgb(206, 255, 232);
      margin: 8px;
    
      li {
        list-style-type: none;
        line-height: 24px;

        img
        {
          width: 16px;
          vertical-align: middle;
        }
      }
    }

    .serie
    {
      background-color: rgb(255, 222, 206);
    }
  }

</style>
