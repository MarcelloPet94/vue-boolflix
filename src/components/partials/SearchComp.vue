<template>
  <div class="search_bar">
    <form>
      <input type="text" v-model.trim="inputRicerca" />
      <button
        type="submit"
        @click.prevent="$emit('ricercaFilm', inputRicerca)"
      ></button>
    </form>
  </div>
</template>

<script>
export default {
  name: "SearchComp",
  data() {
    return {
      inputRicerca: "",
    };
  },
};
</script>

<style scoped lang="scss"></style>
