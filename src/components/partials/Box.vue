<template>
    <div class="box">
        <div class="cover_container">
            <img :src="poster" alt="No img">
        </div>
        <h2>{{titolo}}</h2>
        <p>Titolo originale: {{titoriginale}}</p>          
        <ul>
        <li><img :src="bandiera"></li>
        <p class="vote" v-html="valutazione">{{ valutazione }} </p>
        </ul>
    </div>
</template>

<script>

export default {
  name: 'Box',
  props:{
      poster: String,
      titolo: String,
      titoriginale: String,
      bandiera: String,
      valutazione: String,
  }

}
</script>

<style lang="scss">
  .cover_container
  {
    height: 80vh;
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

    .vote
    {
        margin: 8px 0;
        color: red
    }

</style>
