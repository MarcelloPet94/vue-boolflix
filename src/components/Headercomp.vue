<template>
   <div class="nav_container">
     <div class="logo_page">
       <h2>BOOLFLIX</h2>
     </div>

    <div class="search_camp">     
        <SearchComp
        @ricercaFilm = "passaDaHeader"
        />
    </div>        
   </div>
</template>

<script>
import SearchComp from './partials/SearchComp.vue'

export default {
  name: 'Main',
  components: {
    SearchComp,
  },

  methods: {
    passaDaHeader( daHeader )
    {
      this.$emit('arrivaDaHeader' , daHeader)
    }
  }

}
</script>

<style scoped lang="scss">

.nav_container
{
  position: fixed;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 24px;
  background-color: #010101;
  border-bottom: 1px solid lightgray;

  h2
  {
    font-family: sans-serif;
    color: red;
  }
}
</style>
