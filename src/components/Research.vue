<template>
   <div>
      <SearchComp
      @ricercaFilm = "riassegnaDatoRicerca"
      />

      <div class="ricerca_container">
        <div class="box" v-for="film in tuttiFilmData" :key="film.id">
          <div class="cover_container">
              <img :src="ottieniImmagine( film.poster_path )" alt="No img">
          </div>
            <h2>{{film.title}}</h2>
            <p>Titolo originale: {{film.original_title}}</p>          
          <ul>
            <li><img :src="printFlag( film.original_language )"></li>
            <li>Voto:  {{ gestioneVoto( film.vote_average ) }} </li>
          </ul>
        </div>

        <div class="box" v-for="serie in tuttiSerieData" :key="serie.id">
          <div class="cover_container">
            <img :src="ottieniImmagine( serie.poster_path )" alt="No img">
          </div>
            <h3>{{serie.name}} <span class="tv">(Serie TV)</span></h3>
            <p>Titolo originale: {{serie.original_name}}</p>
          <ul>
            <li><img :src="printFlag( serie.original_language )"></li>
            <li>Voto: {{ gestioneVoto( serie.vote_average ) }} </li>
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
      serverImg: 'https://image.tmdb.org/t/p/',
      titolo: '',
      tuttiFilmData : [],
      tuttiSerieData: [],
      validFlags:['it','de','en','fr'],
    }
  },

    methods:{
      riassegnaDatoRicerca(inputRicerca){
        this.titolo = inputRicerca  
        this.listaFilm()
        this.listaTv()
    },

    ottieniImmagine( immagine )
    {
      if(immagine)
      {
        return this.serverImg + 'w342' + immagine
      }
      else
      {
        return 'https://fiscalform.it/wp-content/themes/consultix/images/no-image-found-360x260.png'
      }
    },

    printFlag( bandiera )
    {
        if( this.validFlags.includes( bandiera.toLowerCase() ) )
        {
            return require('../assets/img/' + bandiera + '.png')
        }

    },

    gestioneVoto( voto )
    {
      let nVoti = parseInt(voto / 2)
      console.log('voti ricevuti: ' + nVoti)
      let vuota = ''
      for(let n = 0; n <= nVoti; n++)
      {
           vuota += ' * ';
      }
      return vuota
      
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

  .cover_container
  {
    height: 500px;
    overflow: hidden;
    
    img
    {
      width: 100%;
    }
  }
    .box
    {
      width: 30%;
      min-height: 200px;
      padding: 16px;
    
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
  }

.tv
{
  color: gray;
  margin-left: 8px;
}

</style>
