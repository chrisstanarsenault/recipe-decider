<template>
  <div id="app">
    <app-recipe-picker></app-recipe-picker>
  </div>
</template>

<script>
  import RecipePicker from "./components/RecipePicker.vue";

export default {
  name: 'app',

  components: {
    appRecipePicker: RecipePicker
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
