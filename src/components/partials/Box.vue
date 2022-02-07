<template>
    <div class="box">
        <div class="cover_container">
            <img :src="poster" alt="No img">
        </div>
        <div class="info_thumb">
            <div class="content_info">
                <h2>{{titolo}}</h2>
                <p>Titolo originale: {{titoriginale}}</p>          
                <ul>
                <li><img :src="bandiera"></li>
                <p class="vote" v-html="valutazione">{{ valutazione }} </p>
              </ul>
            </div>
        </div>
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

<style lang="scss" scoped>

*
{
  color: #fff;
}

.box
{
  position: relative;
  z-index: 0;
}
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
    margin: 16px;
  
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

.info_thumb
{
  display: none;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  padding: 16px;  
  background-color: #010101;
  border: 1px solid #fff;

  .content_info
  {
    position: absolute;
    bottom: 8px;
  }
}

.box:hover .info_thumb
{
  display: block;
}

.vote
{
    margin: 8px 0;
    color: red
}

</style>
