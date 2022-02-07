<template>
   <div>


      <div class="ricerca_container">
        
        <Box v-for="film in passafilm" :key="film.id"
        
        :poster="ottieniImmagine( film.poster_path )"
        :titolo="film.title"
        :titoriginale="film.original_title"
        :bandiera="printFlag( film.original_language )"
        :valutazione="gestioneVoto( film.vote_average )"

        />

        <Box v-for="serie in passaserie" :key="serie.id"
        
        :poster="ottieniImmagine( serie.poster_path )"
        :titolo="serie.name"
        :titoriginale="serie.original_name"
        :bandiera="printFlag( serie.original_language )"
        :valutazione="gestioneVoto( serie.vote_average )"

        />
     
      </div>
      
   </div>
</template>

<script>
import Box from './partials/Box.vue'

export default {
  name: 'Main',
  components: {
    Box,
  },

  props: {
    passaserie : Array,
    passafilm : Array
  },

  data(){
    return{
      validFlags:['it','de','en','fr'], // da modificare ciclando oggetto
      simboloStella: '&#9733;'
    }
  },

  methods:{

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
        else
        {
          return require('../assets/img/en.png')
        }
    },

    gestioneVoto( voto )
    {
      if(voto == 0) { return ' Nessun voto '}
      let nVotiDec = voto / 2
      let nVoti = Math.ceil(nVotiDec)
      console.log('voti ricevuti: ' + nVoti)
      let stelle = ''
      for(let n = 0; n < nVoti; n++)
      {
           stelle += this.simboloStella + ' ';
      }
      
      return stelle
      
    },
  }
}

</script>

<style scoped lang="scss">
  .ricerca_container 
  {
    display: flex;
    flex-wrap: wrap;

  }

.tv
{
  color: gray;
  margin-left: 8px;
}

.immagineVuota
{
  border: 1px solid red;
}

</style>
