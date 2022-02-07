<template>
   <div>
      <SearchComp
      @ricercaFilm = "passaDaHeader"
      />
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

</style>
