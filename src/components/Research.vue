<template>
  <div>
      <SearchComp
      @ricercaFilm = "riassegnaDatoRicerca"
      />

      <div class="ricerca_container">
        <ul v-for="film in tuttiFilmData" :key="film.id">
          <li>{{film.title}}</li>
        </ul>
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
      titoloFilm : '',
      tuttiFilmData : []
    }
  },

  created() {
    //this.listaFilm()
  },


  methods:{
    riassegnaDatoRicerca(inputRicerca){
      this.titoloFilm = inputRicerca    
      this.listaFilm()
    },

    // filtravo questo (appunto x domanda)
    listaFilm(){
      axios.get('https://api.themoviedb.org/3/search/movie' , {
        params: {
          api_key : 'b1d73429cc8d9b6cc6dd4b3887ce83df',
          query : this.titoloFilm
        }
      })
      .then((response) => {
        this.tuttiFilmData = response.data.results  
        console.log(response.data.results);
      })
      .catch(function (error) {
        console.log(error);
      });  
    }
  }
}


</script>

<style scoped lang="scss">

</style>
