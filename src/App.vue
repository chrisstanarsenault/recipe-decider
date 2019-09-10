<template>
  <div id="app">
    <app-header></app-header>
    <app-recipe-picker></app-recipe-picker>
  </div>
</template>

<script>
  import RecipePicker from "./components/RecipePicker.vue";
  import Header from "./components/Header.vue";

export default {
  name: 'app',

  components: {
    appRecipePicker: RecipePicker,
    appHeader: Header
  }
}
</script>

<style>
  #app {
    font-size: 10px;
  }
</style>
